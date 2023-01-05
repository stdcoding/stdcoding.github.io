---
layout: post
comments: true
title:  "Bài 3: Comment trong C++"
title2:  "3. Comments trong C++"
date:   2023-01-05 20:32:00
permalink: 2023/01/cpp-basic/variable/
mathjax: true
tags: C++ Cpp cơ bản
categories: C++_Basic
# sc_project: 11213301
# sc_security: 8d50f6a5
img: /assets/introduce/aimldl.png
summary: Comments can be used to explain C++ code, and to make it more readable. It can also be used to prevent execution when testing
---


C++ Comments
Comments can be used to explain C++ code, and to make it more readable. It can also be used to prevent execution when testing alternative code. Comments can be singled-lined or multi-lined.

Single-line Comments
Single-line comments start with two forward slashes (//).

Any text between // and the end of the line is ignored by the compiler (will not be executed).

This example uses a single-line comment before a line of code:

Example
// This is a comment
cout << "Hello World!";