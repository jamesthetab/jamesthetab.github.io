---
layout: post
title:  "Tunnell's Algorithm"
date:   2016-10-5 20:19:28 +0100
categories: jekyll update
---


Congruent number problem
-------------

The [congruent number problem](http://www.math.uconn.edu/~kconrad/blurbs/ugradnumthy/congnumber.pdf) is ancient and asks which positive integers can be the area of a right triangle with all three sides rational. The problem can be approached by rephrasing in terms of rational points on a special family of Elliptic Curves. This allows us to use the machinery of the addition of points on ECs, and also connect to modular forms and finally to Tunnell's Theorem which relates this to the number of integral solutions of a few fairly simple Diophantine equations.

Theorem
--------

For a given square-free integer n, define

$$A_{n} = \#\{(x,y,z)\in {\mathbb  {Z}}^{3}|n=2x^{2}+y^{2}+32z^{2}\}$$

$$B_{n} = \#\{(x,y,z)\in {\mathbb  {Z}}^{3}|n=2x^{2}+y^{2}+8z^{2}\}$$

$$C_{n} = \#\{(x,y,z)\in {\mathbb  {Z}}^{3}|n=8x^{2}+2y^{2}+64z^{2}\}$$

$$D_{n} = \#\{(x,y,z)\in {\mathbb  {Z}}^{3}|n=8x^{2}+2y^{2}+16z^{2}\}$$


Tunnell's theorem states that supposing n is a congruent number,

if n is odd then $$2A_n = B_n$$ and if n is even then $$2C_n = D_n$$. 

Conversely, if the Birch and Swinnerton-Dyer conjecture holds true for elliptic curves of the form 

$$y^2 = x^3 − n^2x$$ these equalities are sufficient to conclude that n is a congruent number.

Code
----------

In this notebook I begin by counting solutions using a simple bound, and then generate square-free congruent numbers. Finally, I throw the squares back in to generate all congruent numbers up to a given bound as ```allcong(-)```.


```python
import math
def number_of_sols(a, b, c, n): #Solves n = ax^2+by^2+cZ^2
    count = 0
    maxx = int((math.sqrt(n/a))) #int naturally takes floor
    maxy = int((math.sqrt(n/b))) #everything positive so 
    maxz = int((math.sqrt(n/c))) #quick bounds such as y^2<n/a...
    for x in range(-maxx,maxx+1):
        for y in range(-maxy,maxy+1):
            for z in range(-maxz,maxz+1):
                if n == a*x*x+b*y*y+c*z*z:
                    count = count+1
    return count
number_of_sols(1,1,1,1)
```




    6




```python
def An(n):
    return number_of_sols(2,1,32,n)
def Bn(n):
    return number_of_sols(2,1,8,n)
def Cn(n):
    return number_of_sols(8,2,64,n)
def Dn(n):
    return number_of_sols(8,2,16,n)

################################################
#The following ONLY WORKS WHEN n IS SQUARE-FREE#
################################################

def OddCong(n):
    return 2*An(n)==Bn(n)
def EvenCong(n):
    return 2*Cn(n)==Dn(n)
```


```python
def prime_factors(n):
    i = 2
    factors = []
    while i * i <= n:
        if n % i:
            i += 1
        else:
            n //= i
            factors.append(i)
    if n > 1:
        factors.append(n)
    return factors
prime_factors(100)

# set() removes duplicates

len(prime_factors(100)) == len(set(prime_factors(100)))

# Tests for unique prime factors (square free) by 
# seeing if the full list of prime factors agrees 
# with the list as a set (when repetition is removed).
```




    False




```python
def squarefreecong(p):
    listsqfrcong =[]
    upto = p
    for n in range(1,upto+1):
        if len(prime_factors(n)) == len(set(prime_factors(n))): #Only proceed if square-free
            if n%2 != 0: #Odd
                if OddCong(n) == 1:
                    listsqfrcong.append(n)
            if n%2 == 0: #Even
                if EvenCong(n) == 1:
                    listsqfrcong.append(n)
    return listsqfrcong

print'The following are the square-free numbers up to 100 which are Congruent:'
squarefreecong(100)
```

    The following are the square-free numbers up to 100 which are Congruent: [5, 6, 7, 13, 14, 15, 21, 22, 23, 29, 30, 31, 34, 37, 38, 39, 41, 46, 47, 53, 55, 61, 62, 65, 69, 70, 71, 77, 78, 79, 85, 86, 87, 93, 94, 95]


These are known as [primitive congruent numbers](https://oeis.org/A006991). 

If I now wish to generate all congruent numbers I look at the squares up to p and then multiply sets before truncating at p.


```python
def squaresupperlim(q):
    list =[]
    for n in range(1, int(math.sqrt(q))+1):
        list.append(n*n)
    return list

squaresupperlim(85) #As an example
```




    [1, 4, 9, 16, 25, 36, 49, 64, 81]




```python
def allcong(n):
    conglist=[]
    for a in squarefreecong(n):
        for b in squaresupperlim(n):
            conglist.append(a*b)
    finallist=[]
    for c in conglist:
        if c <= n:
            finallist.append(c)
    return sorted(finallist)
print(allcong(126))
                
```

    [5, 6, 7, 13, 14, 15, 20, 21, 22, 23, 24, 28, 29, 30, 31, 34, 37, 38, 39, 41, 45, 46, 47, 52, 53, 54, 55, 56, 60, 61, 62, 63, 65, 69, 70, 71, 77, 78, 79, 80, 84, 85, 86, 87, 88, 92, 93, 94, 95, 96, 101, 102, 103, 109, 110, 111, 112, 116, 117, 118, 119, 120, 124, 125, 126]


Compared with downloaded list from OEIS:


```python
CongruentData = [5,6,7,13,14,15,20,21,22,23,24,28,29,30,31,34,37,
 38,39,41,45,46,47,52,53,54,55,56,60,61,62,63,65,
 69,70,71,77,78,79,80,84,85,86,87,88,92,93,94,95,
 96,101,102,103,109,110,111,112,116,117,118,119,
 120,124,125,126]
```


```python
CongruentData == allcong(126)
```




    True



A deep problem (proving that n=1 is not congruent is equivant to the cubic case of FLT using an infinite descent arguemt...) is reduced to quick calculation :-)


```python

```
