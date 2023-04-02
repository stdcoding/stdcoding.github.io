---
layout: post
comments: true
title:  "C++ nâng cao: Làm việc với Smartpointer như thế nào cho đúng?"
title2:  "C++ nâng cao: Làm việc với Smartpointer như thế nào cho đúng?"
date:   2023-04-01 10:08:00
permalink: 2023/03/cpp-advance/lam-viec-voi-smartpointer/
mathjax: true
tags: C++ Smart-Pointer
categories: C++-Advance
# sc_project: 11213301
# sc_security: 8d50f6a5
img: /assets/cpp/cpp-programming-400x250.png
summary: Smartpointer không phải là 1 khái niệm quá mới mẻ trong C++, tuy nhiên nhiều anh em vẫn chưa tận dụng hết khả năng của smartpointer
---
**Trong trang này:**
<!-- MarkdownTOC -->

- [I. Giới thiệu về smartpointer](#-gioi-thieu-ve-smartpointer)
- [II. Cách sử dụng smartpointer](#-cach-khai-bao-su-dung-smartpointer)
- [III. So sánh smartpointer và con trỏ thường](#-so-sanh-smartpointer-va-con-tro-thuong)
- [IV. Một số thắc mắc thường gặp](#-mot-so-thac-mac-thuong-gap)
    - [1. Có nên gán con smartpointer bằng null sau khi sử dụng không?](#-co-nen-gan-null-cho-smartpointer)
    - [2. Lúc nào nên dùng smartpointer, lúc nào dùng con trỏ thường](#-luc-nao-can-xai-smartpointer)

<a name="-gioi-thieu-ve-smartpointer"></a>
## I. Giới thiệu về smartpointer
Smartpointer không phải là 1 khái niệm quá mới mẻ trong C++, tuy nhiên nhiều anh em vẫn chưa tận dụng hết khả năng của smartpointer. Trước khi đi sâu vào nội dung, hãy cùng lướt xem lại 1 chút về khái niệm nhé:
Trong C++, Smart Pointer (con trỏ thông minh) là một lớp đối tượng được sử dụng để quản lý con trỏ đến một đối tượng cụ thể và tự động giải phóng bộ nhớ được cấp phát cho đối tượng đó khi nó không còn được sử dụng.

Các loại Smart Pointer phổ biến trong C++ bao gồm:
1. std::unique_ptr: Smart Pointer này quản lý một con trỏ đến một đối tượng cụ thể và đảm bảo rằng chỉ có một Smart Pointer được sở hữu đối tượng đó tại một thời điểm. Khi Smart Pointer bị hủy, nó tự động giải phóng bộ nhớ được cấp phát cho đối tượng đó.
2. std::shared_ptr: Smart Pointer này cũng quản lý một con trỏ đến một đối tượng cụ thể nhưng cho phép nhiều Smart Pointer cùng sở hữu đối tượng đó. Khi không còn Smart Pointer nào sở hữu đối tượng, bộ nhớ được tự động giải phóng.
3. std::weak_ptr: Smart Pointer này cũng giống như std::shared_ptr, nhưng không sở hữu đối tượng và chỉ cung cấp một cách để kiểm tra xem đối tượng đó còn tồn tại hay không.
Sử dụng Smart Pointer giúp cho việc quản lý bộ nhớ trở nên an toàn hơn, tránh được những lỗi phổ biến như giải phóng bộ nhớ hai lần, truy cập bộ nhớ không hợp lệ sau khi giải phóng bộ nhớ, và giúp tránh được rò rỉ bộ nhớ. Tuy nhiên, cần lưu ý rằng sử dụng Smart Pointer không phải là giải pháp cho tất cả các vấn đề liên quan đến quản lý bộ nhớ và vẫn cần phải cẩn thận trong việc sử dụng chúng.


<a name="-cach-khai-bao-su-dung-smartpointer"></a>
## II. Cách khai báo và sử dụng smartpointer
Để khai báo Smart Pointer, ta cần sử dụng một trong các lớp Smart Pointer có sẵn trong thư viện chuẩn của C++. Hai lớp Smart Pointer phổ biến nhất trong C++ là _std::unique_ptr và std::shared_ptr_.

Ví dụ, để khai báo một unique_ptr, ta có thể sử dụng cú pháp sau:
```C++
std::unique_ptr<int> myPointer = std::make_unique<int>(10);
int myValue = *myPointer;
std::shared_ptr<int> myPointer = std::make_shared<int>(10);
```
Trong trường hợp của shared_ptr, ta có thể sử dụng cú pháp sau để khai báo một shared_ptr:
```C++
std::shared_ptr<int> myPointer = std::make_shared<int>(10);
```
Tương tự như unique_ptr, ta cũng có thể sử dụng toán tử * để truy xuất giá trị mà con trỏ quản lý.

Khi không còn cần sử dụng Smart Pointer, ta không cần phải giải phóng bộ nhớ thủ công bằng cách sử dụng delete. Thay vào đó, khi Smart Pointer ra khỏi phạm vi, nó sẽ tự động giải phóng bộ nhớ mà nó đang quản lý.

Ví dụ sau đây minh họa cách sử dụng Smart Pointer trong C++:
```C++
#include <iostream>
#include <memory>

int main()
{
    // Khai báo unique_ptr
    std::unique_ptr<int> myPointer = std::make_unique<int>(10);

    // Sử dụng con trỏ
    int myValue = *myPointer;

    std::cout << "Giá trị của con trỏ là: " << myValue << std::endl;

    // Khai báo shared_ptr
    std::shared_ptr<int> mySharedPointer = std::make_shared<int>(20);

    // Sử dụng con trỏ
    int mySharedValue = *mySharedPointer;

    std::cout << "Giá trị của shared pointer là: " << mySharedValue << std::endl;

    return 0;
}
Kết quả khi chạy:
```Log
Giá trị của con trỏ là: 10
Giá trị của shared pointer là: 20
```
<a name="-so-sanh-smartpointer-va-con-tro-thuong"></a>
## III. So sánh Smartpointer và con trỏ thường
Smart Pointer và con trỏ thường đều là cách để quản lý bộ nhớ trong C++. Tuy nhiên, chúng có những khác biệt cơ bản sau đây:

1. Quản lý bộ nhớ: Smart Pointer tự động quản lý bộ nhớ cho đối tượng mà nó trỏ đến, trong khi đó con trỏ thường phải được giải phóng bộ nhớ bằng tay.
2. An toàn hơn trong việc quản lý bộ nhớ: Smart Pointer đảm bảo rằng bộ nhớ được giải phóng một cách an toàn khi đối tượng không còn được sử dụng nữa. Trong khi đó, con trỏ thường có thể dẫn đến rủi ro rò rỉ bộ nhớ hoặc truy cập vào bộ nhớ không hợp lệ.
3. Khả năng tái sử dụng bộ nhớ: Con trỏ thường có thể tái sử dụng bộ nhớ, trong khi Smart Pointer không thể.
4. Tính linh hoạt: Con trỏ thường cho phép thực hiện các phép toán tùy ý trên địa chỉ bộ nhớ, trong khi Smart Pointer hạn chế sự linh hoạt này để đảm bảo an toàn quản lý bộ nhớ.
5. Tốc độ: Vì Smart Pointer phải thực hiện nhiều kiểm tra và quản lý bộ nhớ hơn so với con trỏ thường, nên thường sẽ chậm hơn.
Tóm lại, Smart Pointer là một cách để quản lý bộ nhớ an toàn hơn và dễ sử dụng hơn so với con trỏ thường. Tuy nhiên, trong một số trường hợp, sử dụng con trỏ thường vẫn là cách tốt nhất để giải quyết các vấn đề liên quan đến quản lý bộ nhớ.

<a name="-mot-so-thac-mac-thuong-gap"></a>
## IV. Một số thắc mắc thường gặp khi sử dụng smartpointer
<a name="-co-nen-gan-null-cho-smartpointer"></a>
### 1. Có nên gán con smartpointer bằng null sau khi sử dụng không?
Smart pointer được thiết kế để quản lý một con trỏ và tự động giải phóng bộ nhớ được cấp phát khi nó không còn được sử dụng. Việc gán nullptr cho smart pointer sẽ làm mất đi khả năng quản lý con trỏ và sẽ không tự động giải phóng bộ nhớ được cấp phát bởi con trỏ đó. Thay vào đó, khi không muốn smart pointer trỏ đến bất kỳ đối tượng nào, bạn nên sử dụng phương thức _reset_ để giải phóng con trỏ và thiết lập smart pointer thành một trạng thái không trỏ đến đối tượng nào:

Code ví dụ:
```C++
std::unique_ptr<int> ptr = std::make_unique<int>(42);
ptr.reset(); // giải phóng con trỏ và thiết lập smart pointer thành nullptr
```
Vì vậy, kết luận của mình là không nên gán nullptr (hay NULL trong C++03) cho một smart pointer, vì điều này có thể dẫn đến việc truy cập bộ nhớ không hợp lệ (segmentation fault) hoặc gây ra lỗi logic trong chương trình.

<a name="-luc-nao-can-xai-smartpointer"></a>
### 2. Lúc nào nên dùng smartpointer, lúc nào dùng con trỏ thường
Có thể sử dụng Smart Pointer trong hầu hết các trường hợp khi cần quản lý bộ nhớ trong C++. Tuy nhiên, đối với một số trường hợp đặc biệt, sử dụng con trỏ thường vẫn là lựa chọn tốt hơn. Dưới đây là một số lời khuyên về lựa chọn giữa Smart Pointer và con trỏ thường:

- Sử dụng Smart Pointer khi:
1. Bạn cần tạo một đối tượng động và không biết trước khi nào đối tượng đó sẽ bị hủy.
2. Bạn muốn đảm bảo an toàn khi quản lý bộ nhớ để tránh các vấn đề như rò rỉ bộ nhớ hoặc truy cập vào bộ nhớ không hợp lệ.
3. Bạn không muốn quan tâm đến việc giải phóng bộ nhớ bằng tay.
4. Bạn muốn chia sẻ quyền sở hữu đối tượng với nhiều Smart Pointer.

- Sử dụng con trỏ thường khi:
1. Bạn cần thực hiện các toán tử trên địa chỉ bộ nhớ trực tiếp.
2. Bạn cần tái sử dụng bộ nhớ.
3. Bạn cần thực hiện việc quản lý bộ nhớ theo cách riêng của mình (tuy nhiên, bạn cần phải đảm bảo rằng bộ nhớ được giải phóng một cách an toàn).
4. Bạn muốn tạo ra một cấu trúc dữ liệu tự quản lý.

Tóm lại, khi cần quản lý bộ nhớ, Smart Pointer là một lựa chọn an toàn và dễ sử dụng hơn so với con trỏ thường. Tuy nhiên, trong một số trường hợp đặc biệt, sử dụng con trỏ thường vẫn là lựa chọn tốt hơn.