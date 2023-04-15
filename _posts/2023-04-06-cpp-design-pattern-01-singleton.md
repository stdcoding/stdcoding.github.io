---
layout: post
comments: true
title:  "Design pattern 01: Singleton và những điều bạn chưa biết"
title2:  "Design pattern 01: Singleton và những điều bạn chưa biết"
date:   2023-04-06 22:27:00
permalink: 2023/04/design-pattern/singleton-ban-chua-biet/
mathjax: true
tags: C++ Singleton Design-pattern
categories: Design-pattern
# sc_project: 11213301
# sc_security: 8d50f6a5
img: /assets/images/design-patterns/design-pattern-01-singleton.jpg
summary: Singleton Design Pattern là một trong những mẫu thiết kế phần mềm phổ biến trong lập trình hướng đối tượng
---
**Trong trang này:**
<!-- MarkdownTOC -->

- [I. Giới thiệu về singleton pattern](#-gioi-thieu-ve-singleton-pattern)
- [II. Code mẫu](#-code-mau)
- [III. Những trường hợp thường sử dụng](#-truong-hop-thuong-su-dung)
- [IV. Điểm hạn chế](#-diem-han-che)

<a name="-gioi-thieu-ve-singleton-pattern"></a>

### I. Giới thiệu:
Singleton Design Pattern là một trong những mẫu thiết kế phần mềm phổ biến trong lập trình hướng đối tượng. Nó được sử dụng để giới hạn số lượng đối tượng được tạo ra và đảm bảo rằng chỉ có duy nhất một đối tượng được tạo ra trong suốt quá trình chạy của chương trình.

Trong C++, Singleton Design Pattern có thể được triển khai bằng cách sử dụng một class duy nhất có một phương thức tĩnh trả về tham chiếu đến đối tượng của lớp đó. Điều này đảm bảo rằng chỉ có một đối tượng được tạo ra trong suốt quá trình chạy của chương trình.

<a name="-code-mau"></a>

### II. Code mẫu:
Dưới đây là ví dụ về cách triển khai Singleton Design Pattern trong C++:

```cpp

class Singleton {
public:
    static Singleton& getInstance() {
        static Singleton instance; // đảm bảo chỉ khởi tạo đối tượng một lần
        return instance;
    }

    void showMessage() {
        std::cout << "Hello from Singleton!" << std::endl;
    }

private:
    Singleton() {}; // constructor ẩn để đảm bảo không ai có thể tạo đối tượng bên ngoài class
    Singleton(const Singleton&) = delete; // ngăn chặn sao chép đối tượng
    Singleton& operator=(const Singleton&) = delete; // ngăn chặn gán đối tượng
};
```

Trong đoạn code trên, Singleton là lớp duy nhất được sử dụng để triển khai Singleton Design Pattern. Phương thức tĩnh (static) _getInstance()_ được sử dụng để trả về tham chiếu đến duy nhất một đối tượng được tạo ra trong suốt quá trình chạy của chương trình.

Bên trong phương thức _getInstance()_, đối tượng của lớp Singleton được khởi tạo bằng từ khóa static. Điều này đảm bảo rằng đối tượng chỉ được khởi tạo một lần và được sử dụng bởi tất cả các lời gọi đến phương thức _getInstance()_.

Để đảm bảo chỉ có duy nhất một đối tượng được tạo ra trong suốt quá trình chạy của chương trình, các phương thức tạo và gán đối tượng đã bị xóa bằng cách khai báo chúng là private và ngăn chặn bất kỳ ai có thể sao chép đối tượng bằng cách xóa toàn bộ cơ chế sao chép.



Để hiểu rõ hơn về Singleton Design Pattern, ta có thể xem nó như là một cách để quản lý trạng thái của một đối tượng trong suốt vòng đời của chương trình. Điều này đặc biệt hữu ích khi muốn giảm thiểu việc sử dụng tài nguyên hệ thống hoặc khi muốn tránh tình trạng cạnh tranh nguồn tài nguyên giữa các thread.

<a name="-truong-hop-thuong-su-dung"></a>

### III. Lúc nào thì nên sử dụng singleton:
Singleton Design Pattern thường được sử dụng trong các tình huống sau:

- Truy cập vào tài nguyên chung: Khi muốn truy cập đến tài nguyên chung, như đối tượng kết nối cơ sở dữ liệu hoặc tài nguyên mạng, Singleton Design Pattern có thể được sử dụng để đảm bảo rằng chỉ có một đối tượng được tạo ra để quản lý truy cập đến tài nguyên đó.

- Quản lý trạng thái: Khi muốn quản lý trạng thái của một đối tượng, như đối tượng đếm thời gian hoặc trạng thái của ứng dụng, Singleton Design Pattern có thể được sử dụng để đảm bảo rằng trạng thái được duy trì chính xác trong suốt vòng đời của chương trình.

- Đảm bảo tính duy nhất: Khi muốn đảm bảo rằng chỉ có duy nhất một đối tượng được tạo ra, như khi muốn tránh tình trạng đối tượng bị tạo ra nhiều lần và dẫn đến việc sử dụng tài nguyên không hiệu quả.

<a name="-diem-han-che"></a>

### IV. Điểm hạn chế của singleton

Tuy nhiên là vậy, Singleton Design Pattern cũng có một số hạn chế và điểm yếu:

- Khó để thay đổi: Vì chỉ có duy nhất một đối tượng được tạo ra trong suốt vòng đời của chương trình, nên Singleton Design Pattern khó để thay đổi trong quá trình phát triển.

- Không an toàn cho multi-threading: Nếu không được triển khai đúng cách, Singleton Design Pattern có thể dẫn đến tình trạng cạnh tranh nguồn tài nguyên giữa các thread.

- Không đảm bảo tính đóng gói: Vì Singleton Design Pattern sử dụng một phương thức tĩnh để truy cập đến đối tượng, nên nó không đảm bảo tính đóng gói trong các thành phần khác của chương trình.

Tóm lại, Singleton Design Pattern là một trong những mẫu thiết kế phần mềm phổ biến và rất hữu ích. Bên cạnh đó cũng còn tồn tại những điểm yếu phải yêu cầu ngườI sử dụng phân tích và đánh giá trước khi quyết định đưa vào sử dụng hay không.