___
- JavaScript sử dụng Type conversion(chuyển đổi dữ liệu từ kiểu dữ liệu này sang kiểu dữ liệu khác) để ép giá trị bất kỳ thành một giá trị Boolean trong một ngữ cảnh yêu cầu giá trị Boolean.
- Truthy và falsy là những giá trị mà JavaScript khi ép về kiểu Boolean, hoặc trong một ngữ cảnh Boolean, nó sẽ cho ra giá trị true hoặc false.

##### 1 . Các giá trị được xem là truthy: chuỗi khác rỗng, số khác 0 và tất cả các object. // Bao gồm cả [ ] và { } vì mảng rỗng và chuỗi rỗng vẫn là object.

![[Pasted image 20260512220836.png]]

Ví dụ về giá trị Truthy (nó sẽ bị ép buộc thành True trong ngữ cảnh Boolean và do đó thực thi khối If):
![[Pasted image 20260512220928.png]]
![[Pasted image 20260512220936.png]]

##### 2. Các giá trị được xem là falsy: undefined, null, false, 0, -0, 0n, NaN, ‘’.
![[Pasted image 20260512221020.png]]

Ví dụ về giá trị Falsy (Nó sẽ bị ép thành kiểu False trong một ngữ cảnh boolean và do đó bỏ qua khối If.
![[Pasted image 20260512221044.png]]

- Một ví dụ nữa về Truthy và Falsy trong một ngữ cảnh Boolean. Ở đây toán tử || sẽ trả về toán hạng vế trái nếu vế trái là truthy còn nếu vế trái là falsy thì nó sẽ trả về toán hạng vế phải (cách này thường được dùng để cung cấp giá trị mặc định). 
- Nhưng nó cũng sẽ xảy sau một số vấn đề như bên dưới mà bạn dễ dàng nhận thấy được nếu bạn coi 0, ‘’, NaN là hợp lệ. 
- Như person.point ở đây có giá trị 0 (falsy) nên nó sẽ trả về toán hạng bên phải là undefined point gây ra kết quả không mong muốn. 
- Cách khắc phục, nullish coalescing operator (??) là một tính năng mới được giới thiệu trong ES11(ECMAScript 2020). 
- Theo định nghĩa của MDN ?? là một toán tử logic sẽ trả về toán hạng bên phải nếu vế trái là null hoặc undefined, và nếu không thì sẽ trả về toán hạn bên trái của nó. Như vậy nếu giá trị là 0, ‘’, NaN thì nó vẫn sẽ chấp nhận là các giá trị hợp lệ.
![[Pasted image 20260512221212.png]]
