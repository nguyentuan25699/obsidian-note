---
date: 2026-09-09
tags:
  - backend
  - code
  - learning
draft: false
related:
---
> [!info] Bối cảnh
> Ghi lại toàn bộ mẹo + lỗi thực tế gặp phải khi setup monorepo học backend: 1 repo git chứa 2 project song song — `express-api/` (build tay, tự quyết định từng phần) và `nest-api/` (dựng bằng Nest CLI, có cấu trúc sẵn) — để so sánh trực tiếp cách 2 framework tổ chức code trên cùng 1 bài toán.

## 1. Cấu trúc Monorepo kiểu "học so sánh"

```
nodejs/                  ← 1 git repo duy nhất
├── .gitignore           ← rule chung cho cả 2 project
├── express-api/         ← project độc lập: package.json, node_modules, tsconfig riêng
└── nest-api/            ← project độc lập: package.json, node_modules, tsconfig riêng
```

Mỗi thư mục con là **project độc lập hoàn toàn** — có `package.json` riêng (nên dependency version của project này không ảnh hưởng project kia), `node_modules` riêng, `tsconfig.json` riêng. Điểm chung duy nhất là cả hai nằm trong 1 git repo, để tiện commit song song 2 bên khi làm cùng 1 tính năng (vd cùng thêm CRUD `products`) và diff trực tiếp cách viết khác nhau giữa Express và Nest cho cùng 1 yêu cầu.

Đây là 1 dạng đơn giản của **monorepo** — khác với monorepo "chuẩn" ở công ty lớn (thường có tool quản lý riêng như Turborepo/Nx để build/cache/share code giữa các package), ở đây không cần tool gì thêm vì 2 project hoàn toàn tách biệt, không share code với nhau.

## 2. TypeScript config cho Node backend

Khác với frontend (Next.js/CRA đã cấu hình sẵn `tsconfig.json` hợp lý), viết backend từ đầu bằng TypeScript thì phải tự hiểu và tự set từng field. Những field quan trọng nhất:

```json
{
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist",
    "module": "nodenext",
    "target": "esnext",
    "types": ["node"],
    "strict": true
  }
}
```

- **`rootDir` / `outDir`** — tách biệt rõ ràng thư mục chứa source code (`src/`) và thư mục chứa kết quả sau khi biên dịch (`dist/`). `dist/` là output tự sinh ra từ `src/`, không bao giờ nên commit vào git (đã đưa vào `.gitignore`) — logic giống hệt việc không commit `node_modules`.
- **`module: "nodenext"`** — báo cho TypeScript biết phải resolve import/export theo **đúng cách Node.js thật sự làm ở runtime** (tôn trọng field `"type"` trong `package.json`, đòi hỏi ghi rõ đuôi file khi import ở ESM...). Đây là điểm khác biệt lớn so với cấu hình `module` mặc định khi làm frontend với bundler (Webpack/Vite/Next) — bundler có cách resolve module riêng, "dễ dãi" hơn Node runtime thật rất nhiều (tự động thêm đuôi file, tự động resolve `index.ts`...).
- **`target: "esnext"`** — cho phép dùng cú pháp JavaScript mới nhất khi biên dịch, vì Node runtime hiện đại (bản 26.x đang dùng) đã hỗ trợ hầu hết tính năng ES mới, không cần "hạ cấp" cú pháp xuống bản cũ như khi build cho trình duyệt (nơi vẫn cần hỗ trợ trình duyệt cũ).
- **`strict: true`** — bật toàn bộ các check nghiêm ngặt của TypeScript (không cho `any` ngầm định, bắt buộc check `null`/`undefined`...). Nên luôn bật ngay từ đầu dự án — bật muộn sau này sẽ phải sửa rất nhiều lỗi type dồn lại một lúc.

> [!bug] Cạm bẫy: `"types": []`
> Một số cách tạo `tsconfig.json` (kể cả `npx tsc --init` ở vài phiên bản) generate sẵn dòng `"types": []` (mảng rỗng) kèm comment gợi ý. Nếu để nguyên mảng rỗng này, TypeScript sẽ **không nạp bất kỳ type global nào của Node nữa** — kể cả khi đã cài `@types/node` đầy đủ, các biến toàn cục quen thuộc như `process`, `__dirname`, `Buffer`, `console`... đều báo lỗi "Cannot find name". Luôn phải set rõ `"types": ["node"]` để TypeScript biết cần nạp bộ định nghĩa type của Node vào.

## 3. `tsx` — dev runner gọn cho TypeScript

Khi phát triển, cần 1 công cụ để: (1) chạy trực tiếp file `.ts` mà không cần build ra `.js` trước, và (2) tự động chạy lại mỗi khi sửa code (watch mode). Cách cũ thường phải ghép 2 tool riêng (`ts-node` để chạy TS + `nodemon` để watch). `tsx` gộp luôn cả 2 chức năng vào 1 tool duy nhất, cấu hình đơn giản hơn hẳn:

```json
"scripts": {
  "dev": "tsx watch src/index.ts",
  "build": "tsc",
  "start": "node dist/index.js"
}
```

`dev` dùng khi code (chạy trực tiếp, tự reload). `build` biên dịch TypeScript ra JavaScript thật trong `dist/` theo đúng `outDir` đã cấu hình. `start` chạy bản đã build — đây là lệnh dùng khi deploy thật lên production (không nên chạy `tsx` ở production vì nó phải biên dịch TypeScript "on the fly" mỗi lần chạy, tốn hiệu năng hơn chạy thẳng file `.js` đã build sẵn).

## 4. Yarn 4 (Berry) — chế độ PnP

> [!tip] PnP là gì
> Yarn 4 mặc định chạy chế độ **PnP (Plug'n'Play)**: thay vì tạo thư mục `node_modules` chứa hàng nghìn file như cách truyền thống, Yarn giữ toàn bộ package đã tải trong 1 cache tập trung (thường ở global, ngoài project), rồi sinh ra 1 file duy nhất `.pnp.cjs` đóng vai trò "bản đồ" — map thẳng mỗi tên package sang đúng vị trí file thật trong cache đó khi code gọi `require`/`import`. Lợi ích: cài đặt nhanh hơn (không copy file trùng lặp giữa các project), tránh được lỗi "phantom dependency" (import nhầm 1 package không thật sự khai báo trong `package.json` nhưng vẫn chạy được vì nó nằm lẫn đâu đó trong `node_modules` do 1 package khác kéo về). Đây là hành vi bình thường của Yarn 4 — thấy thư mục project không có `node_modules` sau khi `yarn install` xong thì đừng hoảng, kiểm tra có file `.pnp.cjs` là biết cài đặt đã thành công.

Muốn quay lại kiểu `node_modules` truyền thống (một số editor/tool cũ chưa hỗ trợ tốt PnP, hoặc muốn dễ debug bằng cách mở thẳng file trong `node_modules`), tạo file `.yarnrc.yml` ở gốc project:

```yaml
nodeLinker: node-modules
```

> [!bug] Lỗi thật đã gặp: Yarn patch không tương thích TypeScript 7
> ```
> Error: typescript@patch:...builtin<compat/typescript>: ENOENT: no such file or directory,
> lstat '.../typescript/lib/_tsc.js'
> ```
> **Nguyên nhân thật**: Yarn 4 có sẵn 1 bộ "patch" nội bộ (built-in) cho một số package phổ biến — trong đó có `typescript` — để chỉnh sửa nhẹ package đó cho tương thích với cơ chế PnP. Patch này được viết dựa theo **cấu trúc thư mục nội bộ cũ** của package `typescript`. TypeScript bản 7.0.2 (bản viết lại engine bằng Go, thay đổi hoàn toàn cách đóng gói file bên trong) đã đổi cấu trúc thư mục đó — patch cũ của Yarn tìm đúng đường dẫn file cũ (`lib/_tsc.js`) nhưng file đó không còn tồn tại nữa ở cấu trúc mới → lỗi.
>
> **2 giả thuyết sai đã thử trước khi tìm ra nguyên nhân thật**:
> 1. Tưởng do chế độ PnP gây ra → đổi sang `nodeLinker: node-modules` — **lỗi y hệt không đổi**, chứng minh giả thuyết sai (nếu đúng do PnP thì đổi linker phải hết lỗi).
> 2. Tưởng do lúc đầu chạy `npm init` thay vì `yarn init` để lại "tàn dư" gì đó → sai, vì `package.json` chỉ là 1 file JSON thuần, không quan trọng ai/tool nào tạo ra nó, Yarn đọc file này giống hệt nhau bất kể nguồn gốc.
>
> **Fix thật**: downgrade về bản TypeScript ổn định hơn, được Yarn hỗ trợ tốt hơn (bản 5.x, chưa đổi sang engine Go):
> ```bash
> yarn remove typescript
> yarn add -D typescript@^5.7.0
> ```
>
> **Bài học debug quan trọng**: khi đổi 1 giả thuyết (ở đây là PnP → node-modules) mà **lỗi giữ nguyên y hệt, không hề thay đổi**, đó là tín hiệu mạnh cho thấy giả thuyết đó sai — nguyên nhân thật nằm ở chỗ khác hoàn toàn. Nên đọc kỹ toàn bộ nội dung message lỗi thay vì chỉ nhìn dòng đầu: ở đây version number `7.0.2` xuất hiện ngay trong đường dẫn của lỗi — đó chính là manh mối quan trọng nhất, chỉ thẳng tới nguyên nhân thật.

## 5. Express vs Nest CLI — khác biệt lúc scaffold

| | `express-api/` (build tay) | `nest-api/` (Nest CLI) |
|---|---|---|
| Cách tạo | `npm/yarn init` thủ công, tự thêm từng thứ một | `npx @nestjs/cli new nest-api` — 1 lệnh sinh ra full project |
| Cấu trúc thư mục | Tự quyết định 100%, không ai ép | CLI ép theo cấu trúc chuẩn (`src/main.ts`, `app.module.ts`, `app.controller.ts`, `app.service.ts`) |
| Dependencies core | Chỉ `express` | `@nestjs/common`, `@nestjs/core`, `@nestjs/platform-express` (**Nest chạy trên Express bên dưới theo mặc định!**), `reflect-metadata` + `rxjs` (bắt buộc để decorator và Observable của Nest hoạt động) |
| Lint/test/format | Phải tự cài nếu muốn (ESLint, Prettier, Jest...) | ESLint + Prettier + Jest có sẵn, cấu hình sẵn ngay từ lúc scaffold |
| Tên script chạy dev | Tự đặt tuỳ ý (ở đây đặt là `dev`) | Theo quy ước cố định của Nest: `start:dev` |

> [!tip] Insight cho việc học tiếp
> Sự khác biệt "tự do hoàn toàn" (Express) vs "bị ép theo khuôn" (Nest) chính là điều sẽ được đào sâu ở **Tuần 3 — Kiến trúc & Dependency Injection**: Nest ép cấu trúc Module/Controller/Service + injection ngay từ lúc khởi tạo project, trong khi Express để mặc định hoàn toàn tự do, muốn có cấu trúc tương tự phải tự thiết kế và tự kỷ luật giữ theo.

## 6. Cạm bẫy: Nest CLI tự động `git init`

> [!bug] Git repo lồng bên trong monorepo
> Khi chạy `nest new`, CLI tự động chạy `git init` **bên trong** thư mục project vừa tạo ra — kết quả là có **1 git repo con nằm lồng bên trong git repo cha** (repo cha là repo chung của cả monorepo, đã tạo từ trước). Hậu quả cụ thể: ở repo cha, lệnh `git status` sẽ **không** liệt kê từng file bên trong `nest-api/` như bình thường (như nó vẫn làm với `express-api/`) — mà chỉ hiện gọn đúng 1 dòng `?? nest-api/`, coi cả thư mục đó là 1 khối chưa track duy nhất, y hệt cách git hiển thị 1 **git submodule**.
>
> **Vì sao lại vậy**: git coi bất kỳ thư mục nào chứa `.git` riêng là ranh giới của 1 repo khác, nó sẽ không "nhìn xuyên" vào bên trong repo con đó để track từng file lẻ, dù không có khai báo `.gitmodules` chính thức.
>
> **Fix**: xoá `.git` bên trong `nest-api/` (an toàn tuyệt đối nếu repo con đó chưa hề có commit nào — kiểm tra bằng `git -C nest-api log`, nếu báo "does not have any commits yet" thì chắc chắn xoá được, không mất dữ liệu gì):
> ```bash
> rm -rf nest-api/.git
> ```
> Sau khi xoá, `nest-api/` trở thành 1 thư mục bình thường trong mắt git repo cha — `git add nest-api/` sẽ add từng file lẻ bên trong như mọi thư mục khác.

> [!tip] Cách check nhanh có bị "git lồng" không
> ```bash
> git add --dry-run nest-api/
> ```
> Nếu lệnh này chỉ in ra đúng 1 dòng `add 'nest-api'` (không liệt kê chi tiết từng file con bên trong) → dấu hiệu nghi ngờ có `.git` lồng bên trong, cần kiểm tra tiếp bằng `ls -la nest-api/.git`.

## 7. `.gitignore` — checklist cho project Node/TypeScript

```gitignore
node_modules/
dist/
.env
*.log
**/.yarn/install-state.gz   # cache trạng thái cài đặt của Yarn, tự sinh lại được mỗi lần install, không nên commit
```

Nguyên tắc chung để quyết định 1 file/thư mục có nên vào `.gitignore` hay không: **nếu nó tự sinh lại được 100% chỉ từ những file khác đã có trong repo** (như `node_modules` sinh lại từ `package.json` + lockfile, `dist` sinh lại từ `src` qua lệnh build), thì không cần commit — commit nó chỉ làm phình repo và dễ gây xung đột (conflict) vô nghĩa khi nhiều người cùng làm việc.

> [!tip] File cần commit khi dùng Yarn PnP
> Khác với `node-modules` linker (chỉ cần commit `package.json` + lockfile là đủ để người khác cài lại), chế độ **PnP** còn cần commit thêm 2 file `.pnp.cjs` và `.pnp.loader.mjs` — đây là 2 file Node **thực sự cần dùng lúc chạy app** (chúng chính là "bản đồ" resolve module đã nói ở mục 4), không phải file build tạm thời — đừng lỡ tay liệt chúng vào `.gitignore`.

## 8. Git workflow — lỗi hay gặp khi push lần đầu

> [!bug] `error: src refspec main does not match any`
> Xảy ra khi đã chạy đủ 3 lệnh `git remote add origin ...` → `git branch -M main` → `git push -u origin main`, nhưng **quên mất chưa từng chạy `git commit`** lần nào — nghĩa là branch `main` lúc đó đang hoàn toàn rỗng (0 commit), không có gì để đẩy lên remote cả. Git báo lỗi đúng nghĩa đen: "refspec main không khớp với bất kỳ thứ gì" — vì trên local, branch `main` với 0 commit thực chất còn chưa tồn tại thật sự.
>
> **Cách chẩn đoán nhanh**: chạy `git log --oneline -5`, nếu thấy báo `does not have any commits yet` → xác nhận chính xác đây là nguyên nhân.
>
> **Thứ tự đúng cần nhớ**, luôn phải **commit trước khi push**:
> ```bash
> git init
> git add .
> git commit -m "init project"
> git branch -M main
> git remote add origin <url>
> git push -u origin main
> ```

## Liên quan
- [[Tuần 1 - Node.js Fundamentals]]
- [[Express - Nest]]
