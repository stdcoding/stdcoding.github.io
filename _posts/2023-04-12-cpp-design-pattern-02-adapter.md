---
layout: post
comments: true
title:  "Design pattern 02: Adapter design pattern"
title2:  "Design pattern 02: Adapter design pattern"
date:   2023-04-06 22:27:00
permalink: 2023/04/design-pattern/adapter-design-pattern/
mathjax: true
tags: C++ Adapter Design-pattern
categories: Design-pattern
# sc_project: 11213301
# sc_security: 8d50f6a5
img: /assets/images/design-patterns/Adapter_design_pattern.png
summary: Adapter Design Pattern cho phép các đối tượng khác nhau có thể làm việc cùng nhau một cách dễ dàng thay vì phải sửa đổi mã nguồn
---
**Trong trang này:**
<!-- MarkdownTOC -->

- [I. Giới thiệu về adapter pattern](#-gioi-thieu)
- [II. Code mẫu](#-code-mau)
- [III. Những trường hợp thường sử dụng](#-truong-hop-thuong-su-dung)
- [IV. Kết luận](#-ket-luan)

<a name="-gioi-thieu"></a>

### I. Giới thiệu:
Adapter Design Pattern là một trong những mẫu thiết kế phần mềm phổ biến nhất trong lập trình hướng đối tượng. Nó cho phép các đối tượng khác nhau có thể làm việc cùng nhau một cách dễ dàng, thay vì phải sửa đổi mã nguồn hoặc tạo ra các đối tượng mới để phù hợp với nhau. Trong bài viết này, chúng ta sẽ cùng tìm hiểu về Adapter Design Pattern và cách nó có thể được sử dụng trong các dự án phần mềm.

#### Định nghĩa
Adapter Design Pattern là một mẫu thiết kế cấu trúc cho phép các đối tượng khác nhau có thể tương tác với nhau một cách dễ dàng. Nó cho phép một đối tượng chuyển đổi giao diện của nó để phù hợp với giao diện của một đối tượng khác, đồng thời giữ nguyên tính năng của đối tượng ban đầu.

Adapter Design Pattern được sử dụng khi các đối tượng cần được kết nối với nhau, nhưng giao diện của chúng không tương thích hoặc không thể trực tiếp tương tác với nhau. Thay vì sửa đổi mã nguồn của các đối tượng hoặc tạo ra các đối tượng mới để phù hợp với nhau, Adapter Design Pattern cho phép chúng ta tạo ra một lớp trung gian (adapter) để chuyển đổi giao diện của một đối tượng sang giao diện của đối tượng khác.

##### Các thành phần của Adapter Design Pattern:

Adapter Design Pattern bao gồm ba thành phần chính: Target, Adapter và Adaptee.

![Design pattern adapter](/assets/images/design-patterns/adapter-dp-uml.jpg)

+ _Target_: Là một interface hoặc lớp trừu tượng đại diện cho giao diện mà các đối tượng khác nhau cần kết nối với nhau.
+ _Adapter_: Là một lớp trung gian giúp các đối tượng có thể tương tác với nhau bằng cách chuyển đổi giao diện của chúng. Adapter kế thừa hoặc sử dụng đối tượng Adaptee để thực hiện chuyển đổi giao diện.
+ _Adaptee_: Là đối tượng hiện tại cần được chuyển đổi giao diện để có thể tương tác với các đối tượng khác.

##### Ví dụ về Adapter Design Pattern:

<ul>Để hiểu rõ hơn về Adapter Design Pattern, chúng ta hãy xem xét một ví dụ đơn giản về việc kết nối hai hệ thống khác nhau.

Giả sử chúng ta có hai hệ thống
Hệ thống A: Đang sử dụng một interface I1 để truy xuất dữ liệu từ cơ sở dữ liệu. Interface I1 này không tương thích với hệ thống B.

Hệ thống B: Cần truy xuất dữ liệu từ cơ sở dữ liệu được sử dụng bởi hệ thống A. Tuy nhiên, hệ thống B sử dụng interface I2 để truy xuất dữ liệu từ cơ sở dữ liệu.

Hệ thống A: Đang sử dụng một interface I1 để truy xuất dữ liệu từ cơ sở dữ liệu. Interface I1 này không tương thích với hệ thống B.

Hệ thống B: Cần truy xuất dữ liệu từ cơ sở dữ liệu được sử dụng bởi hệ thống A. Tuy nhiên, hệ thống B sử dụng interface I2 để truy xuất dữ liệu từ cơ sở dữ liệu.

Để kết nối hai hệ thống này, chúng ta cần tạo ra một Adapter để chuyển đổi giao diện từ I1 sang I2. Bằng cách này, hệ thống B có thể sử dụng Adapter để truy xuất dữ liệu từ cơ sở dữ liệu được sử dụng bởi hệ thống A.</ul>
<a name="-code-mau"></a>

### II. Code mẫu

Mã nguồn của Adapter sẽ như sau:

```cpp
public interface I1 {
    public void getData();
}

public interface I2 {
    public void fetchData();
}

public class Adaptee implements I1 {
    public void getData() {
        System.out.println("Getting data from database...");
    }
}

public class Adapter implements I2 {
    private I1 adaptee;

    public Adapter(I1 adaptee) {
        this.adaptee = adaptee;
    }

    public void fetchData() {
        adaptee.getData();
    }
}

```

Ở đây, Interface I1 là Target, Adaptee là đối tượng cần được chuyển đổi giao diện, và Adapter là lớp trung gian giúp chuyển đổi giao diện.

Khi hệ thống B cần truy xuất dữ liệu từ cơ sở dữ liệu được sử dụng bởi hệ thống A, nó sẽ tạo một Adapter và sử dụng phương thức fetchData() để truy xuất dữ liệu từ cơ sở dữ liệu. Adapter sẽ sử dụng đối tượng Adaptee để truy xuất dữ liệu từ cơ sở dữ liệu thông qua phương thức getData().

<a name="-truong-hop-thuong-su-dung"></a>

### III. Những trường hợp thường sử dụng

Adapter Design Pattern thường được sử dụng trong các trường hợp sau:

1. Khi bạn muốn sử dụng một đối tượng có giao diện không tương thích với một đối tượng khác.

2. Khi bạn muốn sử dụng một đối tượng có giao diện cũ nhưng không muốn thay đổi mã nguồn của nó.

3. Khi bạn muốn sử dụng một đối tượng có giao diện mới nhưng không muốn ảnh hưởng đến các đối tượng khác đang sử dụng đối tượng cũ.

4. Khi bạn muốn tách biệt các thành phần của hệ thống để giảm sự phụ thuộc giữa chúng.

*Ví dụ:*

Giả sử bạn đang phát triển một ứng dụng quản lý sản phẩm và có sử dụng hai API để truy xuất thông tin sản phẩm: một API cũ đã được sử dụng trong ứng dụng của bạn từ lâu và một API mới được phát triển gần đây. Tuy nhiên, hai API này có giao diện khác nhau, điều này gây khó khăn cho việc tích hợp chúng vào ứng dụng của bạn.

Trong trường hợp này, bạn có thể sử dụng Adapter Design Pattern để tạo ra một Adapter để chuyển đổi giao diện từ API cũ sang API mới. Bằng cách này, bạn có thể tiếp tục sử dụng API cũ mà không cần thay đổi mã nguồn của nó và tích hợp API mới vào ứng dụng của bạn một cách dễ dàng.

<a name="-ket-luan" ></a>

### IV. Kết luận

Adapter Design Pattern là một mẫu thiết kế cấu trúc rất hữu ích trong việc kết nối các đối tượng khác nhau có giao diện không tương thích hoặc không thể trực tiếp tương tác với nhau. Bằng cách sử dụng Adapter Design Pattern, chúng ta có thể tạo ra một lớp trung gian để chuyển đổi giao diện của một đối tượng sang giao diện của đối tượng khác, giúp cho các đối tượng này có thể tương tác với nhau một cách dễ dàng.