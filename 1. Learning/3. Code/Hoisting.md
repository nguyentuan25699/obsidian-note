___
## 1. Hoisting là gì ?
- Hoisting là cơ chế mặc định của JavaScript để di chuyển tất cả các biến và hàm khi khai báo lên đầu scope trước khi chúng được thực thi.  
(*Lưu ý đối với cơ chế này nó chỉ di chuyển khai báo, còn việc gán giá trị thì giữ nguyên.*)

## 2. Hoisting variables
Vòng đời của biến trong javascript bao gồm các giai đoạn sau:
- Khai báo
- Khởi tạo giá trị mặc định
- Gán một giá trị cho biến được khởi tạo  
Tuy nhiên, vì Javascript cho phép ta gán giá trị ngay khi khai báo biến. Đây là cách chúng ta thường làm:
```
var hoist = 500;
```

Với đoạn code sau:
```
console.log(hoist);

var hoist = 500;
```
Kết quả nhận được sẽ là `undefined`, Cơ chế Hoisting của Javasript đã đưa khai báo biến lên trên cùng: 
```
var hoist; \\ hoist mới được khai báo nên giá trị của hoist là undefined.

console.log(hoist);

var hoist = 500;
```

- Khai báo được đưa lên trên cùng, là vị trí cao nhất trong scope hện tại (current scope).  
Ví dụ:
```
 function hoist() {
      console.log(mess);
      var mess ='Hello World!';
}
hoist(); //Output: undefined
```
Function trên tương tự như sau:
```
 function hoist() {
      var mess; // Biến mess được khai báo ở trên cùng của scope fuction hoist()
      console.log(mess);
      var mess ='Hello World!';
}
hoist(); //Output: undefined
```

## 3. Hoisting functions
Trong Javascript có hai loại hàm là:
- Khai báo hàm (Function Declaration)
- Biểu thức hàm (Function Expression)  

Với function declarations thì bạn khai báo bắt đầu là function operator, sau đó gán cho nó một cái tên như ví dụ dưới đây:
```
// Function declaration
function speak() {
	console.log("Hello");
}
```

Còn với function expressions thì bạn tạo một variable sau đó gán cho nó với một anonymous function như ví dụ sau đây:
```
// Function expression
var speak = function () {
	console.log("Hello")
};
```

**Trong Javascript thì Function declarations có thuộc tính Hoisting, còn Function expression thì không.**

Ví dụ:
```
//Function declaration
speak(); //Function declaration có Hoisting nên output là undefined
function speak() {
	console.log("Hello");
}
```

```
// Function expression
speak(); //TypeError: speak is not a function.
var speak = function () {
	console.log("Hello")
};
```
