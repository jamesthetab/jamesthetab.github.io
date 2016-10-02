---
layout: post
title:  "Swift Launch"
date:   2016-10-01 20:19:28 +0100
categories: jekyll update
---

Last week I launched Swift to two yeargroups at my school. The aim of this session was to demonstrate the power (and fun) of Swift Playgrounds, presenting the possibilities of Swift for mathematical discovery, while emphasising the difference between experimentation and proof. We are very fortunate that every pupil at the school has their own iPad (with iOS 10 and hence access to Swift Playgrounds)

To begin we heard Conrad Wolfram’s take on the [crisis in math](http://www.ted.com/talks/conrad_wolfram_teaching_kids_real_math_with_computers?language=en) education and I explained my vision of how Swift (“code in our hands”) can help bridge the gap between the classroom and the real world. 

After introducing the group to the basics of Swift in “Learn to Code  1” through to loop, I introduced [Gauss’ famous sum](https://goo.gl/PH40Iz), and in real time I wrote code (complete with typos and helpful red blob suggestions) as calculation. I showed how we could modify our code into a function using the beautiful idea of reversing the order of the numbers and pairing.

We then modified our loop to add odd numbers. It seems the sum of odd numbers yields a square. After checking a few more cases it soon became hard to see if the sum was still a square, so we square-rooted (after importing the Foundation package). We could easily adapt our code to check the first 1000 cases, which indeed were all squares. A very believable conjecture is born from this, but the 1001st example could still fail. I then asked the class to study the “proof” diagram below, and explained how computing can guide our conjectures and help build up intuition but only proof is absolute.

<div style="text-align:center" markdown="1">
![png](/assets/OddsSquares.png)
</div>

I was very keen to demonstrate the scalability of Swift, and after shared the heavily annotated code from WWDC 2016, picking out the now familiar loop and functions, I took charge of the [SPRK+](http://www.sphero.com/sprk-plus) robot, and this created a real buzz in the room. The idea that we are doing “proper coding”, the language of Apps and Hackers resonated.

To bring back to mathematics I shared one of the jewels of arithmetic, Euler’s formula, solving the Basel Problem, and giving a power series converging to Pi:

<div style="text-align:center" markdown="1">
![png](/assets/eqn1.png)
</div>

Hence,

<div style="text-align:center" markdown="1">
![png](/assets/eqn2.png)
</div>

Or, as a limit we can work with,

<div style="text-align:center" markdown="1">
![png](/assets/eqn3.png)
</div>

This was implemented using the code below. The “quick graph preview”, within playgrounds, gave a powerful and compelling visualisation of the asymptotic approach to Pi.

<div style="text-align:center" markdown="1">
![png](/assets/eqn4.png)
</div>
