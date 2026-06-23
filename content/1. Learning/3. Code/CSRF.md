## 1. CSRF là gì?
CSRF ( Cross Site Request Forgery) là kỹ thuật tấn công bằng cách sử dụng quyền chứng thực của người dùng đối với một website. CSRF là kỹ thuật tấn công vào người dùng, dựa vào đó hacker có thể thực thi những thao tác phải yêu cầu sự chứng thực. Hiểu một cách nôm na, đây là kỹ thuật tấn công dựa vào mượn quyền trái phép.

CSRF còn được gọi là "session riding", "XSRF"
___

## 2. Lịch sử về tấn công CSRF
Các kiểu tấn công CSRF xuất hiện từ những năm 1990, tuy nhiên các cuộc tấn công này xuất phát từ chính IP của người sử dụng nên log file của các website không cho thấy các dấu hiệu của CSRF. Các cuộc tấn công theo kĩ thuật CSRF không được báo cáo đầy đủ, đến năm 2007 mới có một vài tài liệu miêu tả chi tiết về các trường hợp tấn công CSRF.

Năm 2008 người ta phát hiện ra có khoảng 18 triệu người sử dụng eBay ở Hàn Quốc mất các thông tin cá nhân của mình. Cũng trong năm 2008, một số khách hàng tại ngân hàng Mexico bị mất tài khoản cá nhân của mình.Trong 2 trường hợp kể trên hacker đều sử dụng kĩ thuật tấn công CSRF.
____

## 3. Kịch bản tấn công CSRF
Các ứng dụng web hoạt động theo cơ chế nhận các câu lệnh HTTP từ người sử dụng, sau đó thực thi các câu lệnh này. Hacker sử dụng phương pháp CSRF để lừa trình duyệt của người dùng gửi đi các câu lệnh http đến các ứng dụng web. Điều đó có thể thực hiện bằng cách chèn mã độc hay link đến trang web mà người dùng đã được chứng thực. Trong trường hợp phiên làm việc của người dùng chưa hết hiệu lực thì các câu lệnh trên sẽ được thực hiện với quyền chứng thực của người sử dụng. Ta có thể xét ví dụ sau:

- Người dùng Alie truy cập 1 diễn đàn yêu thích của mình như thường lệ. Một người dùng khác, Bob đăng tải 1 thông điệp lên diễn đàn. Giả sử rằng Bob có ý đồ không tốt và anh ta muốn xóa đi một dự án quan trọng nào đó mà Alice đang làm.
- Bob sẽ tạo 1 bài viết, trong đó có chèn thêm 1 đoạn code như sau:

```HTML
<img height="0" width="0" src="http://www.webapp.com/project/1/destroy">
```

Để tăng hiệu quả che dấu, đoạn mã trên có thể được thêm các thông điệp bình thường để người dùng không chú ý. Thêm vào đó thẻ `img` sử dụng trong trường hợp này có kích thước 0x0 pixel và người dùng sẽ không thể thấy được.

- Giả sử Alie đang truy cập vào tài khoản của mình ở `www.webapp.com` và chưa thực hiện logout để kết thúc. Bằng việc xem bài post, trình duyệt của Alice sẽ đọc thẻ `img` và cố gắng load ảnh từ `www.webapp.com`, do đó sẽ gửi câu lệnh xóa đến địa chỉ này.
- Ứng dụng web ở `www.webapp.com` sẽ chứng thực Alice và sẽ xóa project với ID là 1. Nó sẽ trả về trang kết quả mà không phải là ảnh, do đó trình duyệt sẽ không hiển thị ảnh.

Ngoài thẻ `img`, các thẻ html có thể sử dụng kĩ thuật trên có thể là:

```HTML
<iframe height="0" width="0" src="http://www.webapp.com/project/1/destroy">
```

```HTML
<link ref="stylesheet" href="http://www.webapp.com/project/1/destroy" type="text/css"/>
```

```HTML
<bgsound src="http://www.webapp.com/project/1/destroy"/>
```

```HTML
<background src="http://www.webapp.com/project/1/destroy"/>
```

```HTML
<script type="text/javascript" src="http://www.webapp.com/project/1/destroy"/>
```

Các kĩ thuật CSRF rất đa dạng, lừa người dùng click vào link, gửi email chứa các đoạn mã độc đến người dùng… Hacker còn có thể che giấu các link ở trên rất khéo léo. Ví dụ trong trường hợp thẻ `img`, người dùng có thể nhận ra nếu vào đường link chứa trong

```HTML
<ing src="http://www.webapp.com/project/1/destroy"/>
```

Tuy nhiên, người dùng sẽ rất có phát hiện nếu hacker dùng đường link như sau:

```HTML
<img height="0" width="0" src="http://www.ahackersite.com/abc.jpg"/>
```

và cấu hình lại máy chủ:

```none
Redirect 302/abc.jpg http://www.webapp.com/project/1/destroy"/>
```

Như vậy người dùng sẽ rất khó để có thể phát hiện, vấn đề trách nhiệm phần lớn thuộc về các website của các nhà cung cấp.
___

## 4 Cách phòng chống tấn công CSRF
Dựa trên nguyên tắc của CSRF "lừa trình duyệt của người dùng (hoặc người dùng) gửi các câu lệnh HTTP", các kĩ thuật phòng tránh sẽ tập trung vào việc tìm cách phân biệt và hạn chế các câu lệnh giả mạo.

### 4.1. Phía user
Để phòng tránh trở thành nạn nhân của các cuộc tấn công CSRF, người dùng internet nên thực hiện một số lưu ý sau:

- Nên thoát khỏi các website quan trọng: Tài khoản ngân hàng, thanh toán trực tuyến, các mạng xã hội, gmail, yahoo… khi đã thực hiện xong giao dịch hay các công việc cần làm. (Check - email, checkin…)
- Không nên click vào các đường dẫn mà bạn nhận được qua email, qua facebook … Khi bạn đưa chuột qua 1 đường dẫn, phía dưới bên trái của trình duyệt thường có địa chỉ website đích, bạn nên lưu ý để đến đúng trang mình muốn.
- Không lưu các thông tin về mật khẩu tại trình duyệt của mình (không nên chọn các phương thức "đăng nhập lần sau", "lưu mật khẩu" …
- Trong quá trình thực hiện giao dịch hay vào các website quan trọng không nên vào các website khác, có thể chứa các mã khai thác của kẻ tấn công.

### 4.2 Phía server

Có nhiều lời khuyến cáo được đưa ra, tuy nhiên cho đến nay vẫn chưa có biện pháp nào có thể phòng chống triệt để CSRF. Sau đây là một vài kĩ thuật sử dụng.

#### 4.2.1 Lựa chọn việc sử dụng GET VÀ POST
Sử dụng GET và POST đúng cách. Dùng GET nếu thao tác là truy vấn dữ liệu. Dùng POST nếu các thao tác tạo ra sự thay đổi hệ thống (theo khuyến cáo của W3C tổ chức tạo ra chuẩn http) Nếu ứng dụng của bạn theo chuẩn RESTful, bạn có thể dùng thêm các HTTP verbs, như PATCH, PUT hay DELETE

#### 4.2.2 Sử dụng captcha, các thông báo xác nhận
Captcha được sử dụng để nhận biết đối tượng đang thao tác với hệ thống là con người hay không? Các thao tác quan trọng như "đăng nhập" hay là "chuyển khoản" ,"thanh toán" thường là hay sử dụng captcha. Tuy nhiên, việc sử dụng captcha có thể gây khó khăn cho một vài đối tượng người dùng và làm họ khó chịu. Các thông báo xác nhận cũng thường được sử dụng, ví dụ như việc hiển thị một thông báo xác nhận "bạn có muốn xóa hay k" cũng làm hạn chế các kĩ thuật Cả hai cách trên vẫn có thể bị vượt qua nếu kẻ tấn công có một kịch bản hoàn hảo và kết hợp với lỗi XSS.

#### 4.2.3 Sử dụng token
Tạo ra một token tương ứng với mỗi form, token này sẽ là duy nhất đối với mỗi form và thường thì hàm tạo ra token này sẽ nhận đối số là"SESSION" hoặc được lưu thông tin trong SESSION. Khi nhận lệnh HTTP POST về, hệ thống sẽ thực hiên so khớp giá trị token này để quyết định có thực hiện hay không. Mặc định trong Rails, khi tạo ứng dụng mới:

```Ruby
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception
end
```

Khi đó tất cả các form và Ajax request được tự động thêm sercurity token generate bởi Rails. Nếu security token không khớp, exception sẽ được ném ra.

#### 4.2.4 Sử dụng cookie riêng biệt cho trang quản trị
Một cookie không thể dùng chung cho các domain khác nhau, chính vì vậy việc sử dụng "[admin.site.com](http://admin.site.com/)" thay vì sử dụng "[site.com/admin](http://site.com/admin)" là an toàn hơn.

#### 4.2.5 Kiểm tra REFERRER
Kiểm tra xem các câu lệnh http gửi đến hệ thống xuất phát từ đâu. Một ứng dụng web có thể hạn chế chỉ thực hiện các lệnh http gửi đến từ các trang đã được chứng thực. Tuy nhiên cách làm này có nhiều hạn chế và không thật sự hiệu quả.

#### 4.2.6 Kiểm tra IP
Một số hệ thống quan trọng chỉ cho truy cập từ những IP được thiết lập sẵn


## Tham khảo
- [http://guides.rubyonrails.org/security.html#cross-site-request-forgery-csrf](http://guides.rubyonrails.org/security.html#cross-site-request-forgery-csrf)  
- [http://securitydaily.net/csrf-phan-1-nhung-hieu-ve-biet-chung-ve-csrf/](http://securitydaily.net/csrf-phan-1-nhung-hieu-ve-biet-chung-ve-csrf/)  
- [http://freetuts.net/ky-thuat-tan-cong-csrf-va-cach-chong-csrf-106.html](http://freetuts.net/ky-thuat-tan-cong-csrf-va-cach-chong-csrf-106.html)

