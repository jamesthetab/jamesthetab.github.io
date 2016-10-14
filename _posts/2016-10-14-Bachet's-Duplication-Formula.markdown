---
layout: post
title:  "Bachet's Duplication Formula"
date:   2016-10-14 20:19:28 +0100
categories: jekyll update
---

Bachet’s Equation and Geometry
-------------------

Today’s blog entry concentrates on Diophantine Equations — problems posed in terms of whole numbers, and connected problems over the rationals.  Typically these problems are very easy to understand but difficult to solve.  Their solution often involves leaving the safe world of the integers and using tools and techniques from other areas of mathematics before “projecting” the answer back into whole numbers.  The example I’m going to describe today will use ideas from algebra and geometry.

Fix some integer $$c$$.  What are the rational solutions of the equation

$$y^2 - x^3 = c        \,\,\,\,     (\star)$$

By rational solution, I allow $$x$$ and $$y$$ to be fractions, but not arbitrary reals.  So we are asking for the difference between a square and a cube to be a certain fixed integer.  This is known as Bachet‘s equation, and we will see that its Geometric interpretation is the key to generating solutions.


An amazing property of this equation is the existence of a so-called Duplication Formula.  Discovered by Bachet in $$1621$$, it states that:

Theorem: Bachet
---------------


If $$(x,y)$$ is a solution to $$(\star)$$ with $$x$$ and $$y$$ rational, then

$$\left(\frac{x^4-8cx}{4y^2},\frac{-x^6-20cx^3+8c^2}{8y^3}\right)$$

 is another solution.

That is, if we know one solution then we can build another one, by simply applying the duplication formula.

Notice that verification of this formula is easy, we just plug this expression into Bachet’s equation $$(\star)$$ and check it reduces down to the original statement that $$x$$ and $$y$$ satisfy $$(\star)$$.

But how did anyone come up with this formula?  

Critically, Bachet’s equation is not linear (it contains higher powers of variables — it is not expressible as a combination of xs and ys — geometrically it does not correspond to a straight line).  In Bezout’s equation (which is linear), if we have one solution $$(X,Y)$$ then we can symmetrically tweak the two variables to generate another solution: if $$aX+bY = c$$, then $$a(X+b)+ b(Y-a) = c$$ and so $$(X+b, Y-a)$$ is also a solution.

It seems that Bachet made a guess, an approximation to another solution, and then improved this guess using an iterative method until he reached the duplication formula, but this does not give any intuition on why this formula should work, and purely as a piece of algebra it remains mysterious.

Example: $$y^2-x^3 = -2$$
-------------------

Now let’s work through an example to see how powerful this formula can be.   It’s not too hard to spot the first solution to this equation: $$(3,5)$$ is a solution (because $$5^2 - 3^3 = -2$$).  Then, using the duplication formula,

$$(3,5)$$ is a solution;

$$\left(\frac{129}{10^2},\frac{-38^3}{10^3}\right)$$ is a solution;

$$\left(\frac{2340922881}{7660^2},\frac{113259286337292}{7660^3}\right)$$ is a solution;

…
Already, these solutions are getting very complicated, and it’s unlikely a super-computer would stumble across such a rational solution, even more unlikely would be Bachet spotting these during his work in the $$17$$th Century.

I hope this convinces you that it is really a very powerful formula, but why does it work?  Events later in the 17th century give us a different way to approach the problem which is far more elegant — the invention by Descartes (or at least the user-friendly notation) of coordinate geometry.

We are all happy with how Cartesian Geometry allows geometric problems to be solved algebraically — we have been doing this since we used Pythagoras to calculate distances between points in the plane, but of interest here is how algebraic problems can benefit from Geometric intuition.

For real $$x$$ and $$y$$, Bachet’s Equation, $$(\star)$$, corresponds to a curve in the plane, and rational solutions correspond to the points where both coordinates are rational.

We now make a simple construction which explains the duplication formula:

![alt text](/assets/PQ.jpg "Tangent to the Curve")

Bachet's equation
---------------

For a given solution $$P = (x,y)$$, draw the tangent to the curve at $$P$$.  For $$y\neq 0$$, substituting the equation of the tangent, $$Y = mX = c$$ into the cubic ($$3$$rd power) curve gives a cubic equation $$(#)$$ in $$X$$.  This leads to $$3$$ (possibly repeated) solutions for the $$X$$-coordinate (and corresponding $$Y$$-coordinate) of the point of intersection.

Let $$Q=(\alpha,\beta)$$. Since the tangent intersects twice at $$P$$, we see that the solutions of $$(#)$$ are $$x$$, $$x$$ and $$\alpha$$.

Question What goes wrong for $$y=0$$?

Claim: $$Q$$ is also a rational point, and its coordinates are given by the duplication formula.

Define a curve to be rational if all its coefficients are.  We begin by noting that the gradient of the tangent will be rational, and that it passes through the rational point $$P$$.  So the tangent is a rational line, and the point $$Q$$ is the intersection of a rational curve and a rational line.

Warning: this is not enough to guarantee that $$Q$$ itself is rational.  For example, consider the intersection of the Rational Line $$y=2$$ and the Rational Curve $$y=x^2$$.  The intersection is not a point with rational coordinates.

After substituting for $$y$$ in the cubic curve (using the equation of the tangent line) we are left with a rational cubic $$(#)$$ in the $$x$$-coordinates corresponding to the three points of intersection.

Thus, using the relation between roots and coefficients of a polynomial (sometimes called Viète‘s formula), the sum of the three $$x$$-coordinates is (up to a sign) a quotient of rational coefficients, so the sum of the three $$x$$-coordinates of intersection is rational.

But two of these solutions (intersecting $$P$$ twice) are rational, so the third (at $$Q$$) must be rational also.

Substituting this $$x$$-coordinate into the rational tangent line gives rational $$y$$-coordinate for $$Q$$.

This proves the first part of the claim.

You might like to check that this new point recovers the Duplication formula.  Remember to use the trick summing the three solutions of the cubic.  The alternative, using the two solutions we know to get a quadratic factor which we then factorise out of the cubic, can get messy.  Hints below.

In the language of elliptic curves, given a rational point $$P$$ we are considering the new rational point $$-2P$$.   This process never repeats itself (and so infinitely many rational points may be generated in this way).  If $$(-2)^s P = (-2)^t P$$ for some $$s,t$$, then, subtracting, $$nP=0$$ for some $$n$$ (where $$0$$ denotes the point at infinity).  Such $$P$$ are known as torsion elements.  The Nagell-Lutz theorem tells us that torsion points with rational coordinates must then have integral coordinates.  We can now use unique factorisation of natural numbers to perform “local calculations” (considering remainders modulo different primes p) to show there are no torsion points with integral coordinates on the curve. 

We do have torsion amongst points with real coordinates, though.  For $$y=0, P=(-\sqrt[3]{c},0)$$, $$P$$ is of order $$2$$: $$2P=0$$.  Also, for $$x=0$$, $$P=(0, \pm \sqrt{c})$$, $$P$$ is of order $$3$$: $$3P=0$$.  Reinterpreting as $$-2P=0$$ $$(-2P = P)$$ respectively, can you explain these results geometrically?

We have shown that if there is a single rational solution, then in fact there are infinitely many.  But there are other related questions to think about.

Are there any rational solutions at all?  Or could the curve meander around all the rational points of $$\mathbb{R}^2$$, as the Fermat curve $$x^3+y^3 = 1$$ does?  (Fermat’s last theorem says that the only rational points on the curve $$x^n + y^n = 1$$ are $$(\pm 1, 0), (0,\pm 1)$$ for even $$n \geq 4$$, and $$(0,1), (1,0)$$ for odd $$n \geq 3$$.

What about working over the integers, are there any integer solutions for a given c?

If there is a solution, are there infinitely many?  (Notice that the duplication formula only returns a rational solution even if you start with integers.)

These questions are explored in the excellent book Rational Points on Elliptic Curves by Silverman and Tate, published by Springer UTM in 1992.  (The relevant part is available on Google books.)

Hints
------------

For rational point $$P= (x,y)$$ on curve $$y^2 = c+x^3$$, gradient at $$P$$ is $$\frac{dy}{dx} = \frac{3x^2}{2y}$$.

Equation of tangent $$Y = X.\frac{3x^2}{2y} + (y-\frac{3x^3}{2y})$$.

Substituting, $$Y^2=X^2.\frac{9x^4}{4y^2}+X.\frac{3x^2}{y}$$. $$(y-\frac{3x^3}{2y}) + (y^2-3x^3+\frac{9x^6}{4y^2})=c+X^3$$.

Intersects at $$P$$, $$P$$, and $$Q= (\alpha,\beta)$$, thus sum of roots:

$$x+x+\alpha=\frac{9x^4}{4y^2}$$

$$\alpha = \frac{x^4-8xc}{4y^2}.$$