---
layout: post
title:  "Formatting Tools"
date:   2016-06-18 20:19:28 +0100
categories: jekyll update
---

As I build up this Blog I expect the mathematical content to become more involved, and I am excited to use Mermaid, a typesetting programme for flow diagrams and Gantt charts. I will give an example of a sequence diagram below.

{% mermaid %}
  sequenceDiagram
A->> B: Query
B->> C: Forward query
Note right of C: Meanwhile, I'm still thinking...
C->> B: Response
B->> A: Forward response
{% endmermaid %}

I've also incorporated MathJax to allow me to use LaTex commands to create beautifully typeset mathematics. Either as standalone equations. Pythagoras' Theorem states that in a right triangle with hypotenuse \\(c\\), and other sides \\(a\\) and \\(b\\):

$$a^2 + b^2 = c^2$$

I can also set up inline math such as \\(e^{i \pi} +1 = 0\\).



