---
layout: post
comments: true
title:  "Bài 2: Comment trong C++ 2"
title2:  "2. Comments trong C++"
date:   2022-12-31 20:31:00
permalink: 2022/12/31/comment2/
mathjax: true
tags: General
categories: General
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