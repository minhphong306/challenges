## 30 DRB of Dai Nguyen
- Facebook: https://www.facebook.com/nvdai2401
- Book name: You don't know JS
- Timeline tracking:
    + D1: 05/11
    + D2: 06/11
    + D3: 08/11
    + D4: 09/11
    + D5: 10/11
    + D6: 11/11
    + D7: 13/11
    + D8: 15/11
    + D9: 17/11
    + D10: 18/11
    + D11: 20/11
    + D12: 22/11
    + D13: 23/11
    + D14:
    + D15:
    

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

#3: Chương 2: Scope & Closure
Trước khi tìm hiểu về scope trong JS thì chương này có đề cập lại Lý thuyết biên dịch - Complier Theory
Bao gồm 3 bước trước khi code được thực thi, quá trình này có thể gọi là compilation - biên tập

- Tokenizing/Lexing: chia các chuỗi ký tự ra thành các từ hay các ký tự có nghĩa được gọi là token. Ví dụ: let x = 2; câu lệnh này sẽ được chia nhỏ ra thành các token: var, x, =, 2 và ;. Khoảng trắng - space có được coi là 1 token tùy thuộc vào việc nó có ý nghĩa hay không. Ví dụ với câu lệnh khai báo ở trên nếu có khoảng trắng thì sẽ ko được coi là 1 token vì có space hay ko thì ý nghĩa và chức năng của câu lệnh vẫn không đổi. Nhưng trong trường hợp so sánh 2 chuỗi ký tự có chứa khoảng trắng thì khoảng trắng sẽ được coi là 1 token vì khi so sánh 2 chuỗi ký tự ta phải so sánh từng ký tự của 11 chuỗi với nhau.
- Parsing: đưa các tokens này vào 1 cây của các phần tử lồng nhau (nested elements). Cây này thể hiện cấu trúc ngữ pháp của chương trình, được gọi là Abstract Syntax Tree - AST. Ví dụ có thể xem ở link phía dưới
- Code generation: là quá trình chuyển AST thành mã lệnh mà máy tính có thể thực thi (mã mã lệnh được chuyển thành thì sẽ tùy thuộc vào ngôn ngữ lập trình)

Trên đây chỉ là 3 bước cơ bản để khái quát chung quá trình biên dịch code. Trên thực tế thì quá trình này sẽ phức tạp hơn.
Đối với JS, thì sẽ không có quá trình build code mà code sẽ được biên dịch sang ngôn ngữ máy (machine instructions) trước khi được thực thi trong thời gian rất ngắn (cỡ micro second).
https://www.facebook.com/groups/simple.challenge/permalink/2392181454377051/


#4: CHƯƠNG 2: SCOPE & CLOSURE
Phần này sẽ tìm hiểu về scope trong JavaScript. Phần này viết trong sách hơi khó hiểu nên mình có tham khảo trên Medium và StackOverflow để hiểu rõ hơn.
Scope là 1 bộ các quy tắc tìm kiếm tên các biến theo tên đã được khai báo ở trong scope đó.

Tại sao scope quan trọng?
- Lợi ích chính là sự an toàn (security - chỗ này dịch hơi phò), có nghĩa là 1 biến chỉ có thể được truy cập trong 1 đoạn chương trình nhất định. Với việc sử dụng scope thì ta có thể tránh được những sửa đổi không mong muốn đến biến từ các đoạn chương trình khác
- Tránh xung đột tên biến trong chương trình

Scope chain: nếu engine không được tìm thấy biến trong scope hiện tại thì engine sẽ tiếp tục tìm kiếm biến đó trong scope cha chứa scope hiện tại, và tiếp tục tìm kiếm cho đến scope lớn nhất là global. Nếu engine tìm thấy tên biến thì sẽ stop quá trình tìm kiếm, ngược lại nếu engine không tìm thấy thì sẽ trả về lỗi 'ReferenceError: ... is not defined'

Các loại scope: [references] Medium & StackOverflow
- Global scope: bất cứ biến nào không nằm trong 1 function hoặc block thì nằm trong global scope. Biến này có thể được sử dụng ở mọi nơi trong chương trình
- Local scope or function scope: là scope chứa những biến được khi báo bên trong 1 function. Những biến này chỉ có thể được truy cập bên trong function đó và các nested scope
- Block scope: là scope chứa những biến được khai báo nằm bên trong  curly braces và không thể truy cập từ bên ngoài curly braces. Sử dụng let và const để khai báo biến thì những biến đó sẽ nằm trong block scope
- Nested scope: scope nằm trong 1 scope khác
- Lexical scope hay static scope là scope được định nghĩa tại thời điểm lexing (thời điểm mà câu các câu lệnh được chia nhỏ thành các token có nghĩa là thời điểm biên dịch code). Bằng cách sử dụng lexical scope thì ta có thể xác định được scope của biến bằng cách nhìn vào source code. Trong khi những ngôn ngữ support dynamic scope thì ta không thể xác định được scope cho đến khi code được thực thi. Các ngôn ngữ support lexical scope: C/C++, Java, JavaScript. Perl support dynamic scope.

CÂU HỎI CHO PHẦN NÀY
Khác biệt giữa "undefined" và "is not defined"?
https://www.facebook.com/groups/simple.challenge/permalink/2393127507615779/

#5: CHƯƠNG 2: SCOPE & CLOSURE
Hôm trước Nguyễn Việt Đức có nhắc đến Hoisting và đồng thời phần tiếp của chương này có đề cập đến Hoisting. Ở đây mình chỉ đề cập đến khái niệm, còn các trường hợp hoisting thì mình sẽ dùng hình ảnh để minh họa. Ae xem hình để rõ hơn nhé 

Khi khai báo biến và hàm nằm bất kỳ ở 1 đoạn code nào trong scope đang chứa nó thì sự khai báo sẽ được đưa về đầu scope đó và được xử lý đầu tiên trước khi phần code còn lại được thực thi được gọi là Hoisting.

ĐÁP ÁN CÂU HỎI CỦA NGÀY HÔM QUA
Câu hỏi: Khác biệt giữa "undefined" và "is not defined"?
Câu trả lời: undefined có nghĩa là biến đó đã đc khai báo rồi, nhưng không đc gán giá trị nên default giá trị của biến là undefined.
Not defined là biến đó chưa hề đc khai báo trong scope hiện tại (hay gọi rõ hơn là undeclared)
-from Nguyễn Việt Đức-

CÂU HỎI CHO PHẦN NÀY
Kết quả của console.log trong đoạn code sau:
var employeeId = '1234abe';
(function(){
	console.log(employeeId);
	var employeeId = '122345';
})();
https://www.facebook.com/groups/simple.challenge/permalink/2393917480870115/

#6: CHƯƠNG 2: SCOPE & CLOSURE
Phần này mình sẽ đi sâu vào những ứng dụng thực tế của Closure trong JS (như mong muốn của sếp Do Minh Phong)
Đầu tiên thì chúng ta cùng nhắc lại khái niệm về Closure.

Closure là 1 function vẫn có thể nhớ, tham chiếu và truy cập vào môi trường mà nó tham chiếu đến kể cả khi function đó đã được thực thi. Closure như 1 cái bao chứa 1 function hoặc 1 tham chiếu đi kèm với môi trường nó tham chiếu đến. Giải thích như này vẫn hơi khó hiểu nên mình có để hình ảnh ở dưới

Ứng dụng của Closure: mỗi ứng dụng có hình ảnh minh hoạ ở dưới
- Giải quyết vấn đề dùng var trong loop. Để giải quyết vấn đề này thì cơ bản là ta phải tạo ra 1 scope riêng cho mỗi vòng lặp bằng các cách sau: dùng let thay var, khai báo function ngoài loop, sử dụng IIFE
- Simulating private scopes for variables - mô phỏng phạm vi riêng cho biến: cho phép những hàm khác hoặc biến khác access vào bên trong 1 function mà không thể sửa trực tiếp biến trong function đó mà phải thông qua 1 function khác.
- Function composition - Hàm kết hợp hay Closure Scope Chain.
- Performance:
  + Dùng closure để caching như trong bài này
  + Tránh việc phải khởi tạo lại function bên trong 1 function sau mỗi lần gọi function đó bằng cách dùng prototype (tham khảo từ Mozilla developer)
https://www.facebook.com/groups/simple.challenge/permalink/2395262737402256/

#7: CHƯƠNG 2: SCOPE & CLOSURE
Hôm nay mình đọc đến phần Dynamic scope. Vì JS không có dynamic scope nên phần này chỉ giới thiệu sơ qua về khái niệm và cách code được thực thi trong trường hợp giả sử JS có dynamic scope.

Khái niệm: Dynamic scope không quan tâm đến cái cách và nơi mà hàm và scope được khai báo mà nó chỉ quan tâm đến nới gọi hàm đó. Dynamic scope hoàn toàn trái ngược với Lexical scope vì Lexical scope được định nghĩa tại author-time (mình thì định nghĩa author-time là thời điểm sau khi code được viết) còn Dynamic scope được định nghĩa tại thời điểm code chạy (run-time)
https://www.facebook.com/groups/simple.challenge/permalink/2396567693938427/

#8: Chương 3: this & Object Prototypes
Đầu chương này nhắc lại khái niệm về this và đưa ra 1 số cách sử dụng this. Mình có đưa ra các trường hợp sử dụng this ở ví dụ trong ảnh (nếu thiếu ae bổ sung giúp mình nhé)
this là 1 sự ràng buộc (binding) được tạo ra khi hàm được gọi (in run-time). Object nó tham chiếu đến phụ thuộc vào nơi và cách mà nó được gọi.

Hiểu lầm thường gặp là this tham chiếu đến chính hàm chứa nó.
Mình bonus thêm phần khác biệt giữa call, apply, bind vì nó có liên quan đến cách sử dụng this:
- call(thisArg, arg1, arg2, ...): gọi một hàm với giá trị của this hoặc object và các đối số riêng lẻ
- apply(thisArg, [arg1, arg2, ...]): gọi một hàm với giá trị của this hoặc object  và các đối số là 1 mảng các giá trị
- bind(thisArg, arg1, arg2, ...): trả về 1 hàm mới và cho phép truyền vào  giá trị của this hoặc object và các đối số riêng lẻ

Hàm call và apply là gần giống nhau. Chúng đều gọi hàm trực tiếp. Chỉ khác ở cách truyền đối số vào (với call thì đối số phân cách bởi dấu phẩy comma và với apply thì đối số cho bởi mảng array)

Hàm bind thì hơi khác hơn một chút. Hàm này không gọi hàm trực tiếp mà nó sẽ trả về một hàm mới và có thể sử dụng hàm mới này sau. Về cách truyền tham số vào thì nó giống với hàm call.
https://www.facebook.com/groups/simple.challenge/permalink/2398245823770614/

#9: Chương 3: this & Object Prototypes
Phần này có đề cập đến các kiểu ràng buộc this. Có 5 loại binding-ràng buộc với this. Ae muốn hiểu thêm thì tìm ví dụ trên GG nhé, hnay mình hơi lười thêm ví dụ.
- Default binding - Ràng buộc mặc định: this tham chiếu đến global object. Tuy nhiên, nếu hàm chứa this ở strict mode thì sẽ có lỗi: TypeError: this is undefined.
- Implicit binding - Ràng buộc rõ ràng: this tham chiếu đến object có method là function chứa this khi method đó được gọi bởi object
- Explicit binding - Ràng buộc không rõ ràng: ép ràng buộc this vào 1 function với việc gọi hàm sử dụng call(), aplly(), bind()
- Hard binding - Ràng buộc khó khăn: khi 1 hàm được gọi với kiểu explicit binding và được đặt bên trong 1 hàm khác
- new Binding: sử dụng từ khóa new với constructor (constructor là 1 hàm được gọi cùng với từ khóa new ở phía trước)

https://www.facebook.com/groups/simple.challenge/permalink/2400045776923952/

#10: Chương 3: this & Object Prototypes
Phần này trình bày về object trong js.

Object có 2 kiểu khai báo:
- Declarative form: khai báo object có chứa key và value luôn
- Constructed form: khai báo với từ khóa new Object()

Khác biệt giữa 2 kiểu này là (1) có thể add nhiều key/value từ khi khai báo, trong khi đó (2) chỉ add các key/value từng cặp 1
JS Function được gọi là first class và cũng là 1 object, nó có thể là 1 đối số truyền vào hàm khác, có thể được trả về từ 1 hàm, có thể được dùng để gán cho 1 biến

Built-in objects: String, Number, Object, Array, Symbol, Boolean, Function, Date, RegExp, Error
https://www.facebook.com/groups/simple.challenge/permalink/2400924020169461/

#11: chia sẻ về First class function

Theo yêu cầu của Nguyễn Việt Đức yêu cầu chia sẻ về First class function trong js thì hôm nay mình sẽ nói ngắn gọn về First class function js. Tuy ngắn gọn nhưng đọc 1 lần là hiểu và nhớ ngay nhé (Đọc ví dụ cụ thể trong bài đính kèm).
First class function (FCF) là function có thể lưu trữ bởi 1 biến, bởi 1 vài data stucture như mảng hoặc object, truyền vào 1 hàm khác, được trả về từ 1 hàm khác, thậm trí có thể giữ properties (constructor).

Những ứng dụng hay gặp của FCF:
- Higher-order function: Là  hàm có tham số truyền vào là 1 function hoặc return lại 1 function hoặc có thể nói nó làm việc dựa trên 1 function khác. Ví dụ như hàm: map(), filter(), findIndex()
- Callback cũng là 1 ứng dụng của FCF được dùng khi muốn lắng nghe event, đọc file bất đồng bộ hoặc gọi AJAX req,...

Nguồn tham khảo: https://medium.com/launch-school/javascript-weekly-an-introduction-to-first-class-functions-9d069e6fb137
https://www.facebook.com/groups/simple.challenge/permalink/2401923050069558/

#12: Chương 3: this & Object Prototypes

Hôm nay tìm hiểu về prototype trong js. Phần này khá phức tạp và dài nên phải đọc lại lần nữa. Hôm nay, mình sẽ "spoil" trước 1 chút, bài sau sẽ nói sâu hơn và có những ví dụ cụ thể hơn.
prototype hay __proto__ là 1 thuộc tính ẩn của object tham chiếu đến 1 obj khác.

Prototype chain là cũng giống như scope chain, là quá trình tìm kiếm 1 biến trong 1 obj nếu ko thấy biến đó trong obj hiện tại thì engine sẽ tiếp tục tìm kiếm trong __proto__ của nó, và cứ tiếp tục cho đến khi tìm thấy biến đó. Vậy khi nào thì prototype chain kết thúc? Khi engine tìm kiếm đến Object.prototype mà vẫn ko thấy biến cần tìm và trả về undefined.

Kiểm tra obj1 là prototype của obj2: obj1.isPrototypeOf(obj2)
https://www.facebook.com/groups/simple.challenge/permalink/2403728359889027/

#13: Chương 3: this & Object Prototypes
Chương 3: this & Object Prototypes
Phần tiếp theo tìm hiểu về  khái niệm ''Class Function'' trong js.

Trước tiên ta cần hiểu class trong JS ko giống như class trong các OOP language khác, JS chỉ có object và class chỉ là 1 dạng design pattern.
Class function - cái tên này hơi gây confuse nhưng ae có thể hiểu từ class đưa vào trước function để làm cho mình liên tưởng đến các tính chất của class trong các ngôn ngữ khác như tính kế thừa chẳng hạn. Còn function thì ở đây không phải là những fucntion bình thường mà là những function được sử dụng để khởi tạo đối tượng mới bằng cách sử dụng từ khóa new thì function ở đây được gọi là constructor.

Mọi Object được tạo bằng cách khai báo với từ khóa new sẽ có prototype link với object cha. Khi đó prototype của obj con chính là object cha .prototype. Vì vậy trong js thì ta có thể tạo ra nhiều object có prototype link đến cùng 1 object, chúng liên kết với nhau chứ không phải copy nhau. Cơ chế này được gọi là prototypal inheritance

Inheritance trong js các ngôn ngữ khác có nghĩa là obj con copy object cha. Nhưng trong js thì chúng link với nhau chứ không copy.

Câu hỏi của Nguyễn Việt Đức ở bài trước về prototype khi extend class thì đúng như chú đoán nhưng a muốn có cái nhìn sâu và chi tiết hơn vì cú pháp đó là của ES6 còn sâu về bản chất thì còn nhiều cái behind the scene, haha. Nên các bài tiếp theo sẽ tập trung nói sâu về class trong js hơn.  
https://www.facebook.com/groups/simple.challenge/permalink/2405534816375048/

```