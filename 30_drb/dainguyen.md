## 30 DRB of Dai Nguyen
- Facebook: https://www.facebook.com/nvdai2401
- Book name: You don't know JS

### List
```
#1: Ngày đầu với Chapter 1: Up & Going

- Object.create(obj): tạo 1 object mới từ obj và dùng obj như 1 prototype
    let obj1 = obj2: obj2 ref to obj 1. Nếu thay đổi giá trị của 1 property của obj1 or obj2 thì cái còn lại sẽ ref theo
    let obj2 = Object.create(obj1): obj2 sẽ được kế thừa những property or methods của obj1 và ko modify được

- Kiểu giá trị trong js: 
    string, number, object, boolean, null, undefined, symbol
    Falsy value: "", 0, -0, NaN, null, undefined, false
- So sánh object trong js là so sánh reference. 2 object bằng nhau khi cùng tham chiếu đến cùng 1 object (Xem 2 ảnh dưới để hiểu rõ hơn)
- Hoisting: mọi biến or func khi được khai báo với var sẽ được đưa về đầu scope đang chứa nó khi code được thực thi
https://www.facebook.com/groups/simple.challenge/permalink/2389590727969457/

#2: Chương 1: Up & Going

Hôm nay mình đã tìm hiểu cơ bản và sơ qua về 3 khái niệm IIFE, this và closure. Trong chương này chỉ trình bày sơ qua về các khái niệm để dẫn dắt vào các các chương tiếp theo. Chương kế tiếp sẽ tiết lộ những cái hay ho và xịn xò về Scope & Closure

- IIFE - Immediately Invoked Function Expressions: được execute ngay, có scope riêng và không làm ảnh hưởng đến đến code bên ngoài scope. Ứng dụng trong webpack, sau khi webpack transplie code ES module → ES5 or JS lower code.
- Closure: là khi 1 function vẫn có thể nhớ, tham chiếu và truy cập vào scope của nó kể cả khi function đó đã được thực thi (xem ảnh phía dưới để hiểu rõ hơn về closure). Ứng dụng trong module khi mà 1 hàm được khai báo trong 1 scope này có thể sử dụng trong 1 file và scope khác.
- this: nếu 1 function có sử dụng this, thì this sẽ tham chiếu đến 1 object và object  đó phụ thuộc vào cách function đó được gọi (this sẽ được trình bày chi tiết trong chương 3 nhóe).

Kết thúc Chương 1: Up & Going
https://www.facebook.com/groups/simple.challenge/permalink/2390415464553650/

```