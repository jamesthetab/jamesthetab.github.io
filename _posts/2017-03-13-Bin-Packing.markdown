---
layout: post
title:  "Bin Packing"
date:   2017-03-13 20:19:28 +0100
categories: jekyll update
---


In this introduction to I look at four different algorithms and then compare their efficiency (in terms of number of bins required).

Throughout I use the idea that a bin is open if we've already put at least one item into it.

Before we begin looking at algorithms I import the random number generator and create a short list to work with.


```python
import random
X = random.sample(range(10), 10)
print(X)
```


```python
X = [6, 1, 5, 2, 0, 8, 7, 3, 4, 9]
```

## Next Fit Algorithm

If the item fits in the same bin as the previous item put it there. Otherwise open a new bin and put it there.

I begin at creating a particular instance of the algorithm, and then make into a function.


```python
n = 10 #bin size

print(X)

A = []
Y = X

A.append([Y[0]])
Y.remove(Y[0])

for y in Y:
    if sum(A[-1]) + y <= n: #if y fits in the current bin put it in
        A[-1].append(y)
    else:
        A.append([y])    #otherwise create a new list with it in
    print(A)

```

    [6, 1, 5, 2, 0, 8, 7, 3, 4, 9]
    [[6, 1]]
    [[6, 1], [5]]
    [[6, 1], [5, 2]]
    [[6, 1], [5, 2, 0]]
    [[6, 1], [5, 2, 0], [8]]
    [[6, 1], [5, 2, 0], [8], [7]]
    [[6, 1], [5, 2, 0], [8], [7, 3]]
    [[6, 1], [5, 2, 0], [8], [7, 3], [4]]
    [[6, 1], [5, 2, 0], [8], [7, 3], [4], [9]]



```python
def nextfit(X,n):  #inputs both a list and a size of bin
    n = 10 #bin size
    
    A = []
    Y = X

    A.append([Y[0]])
    Y.remove(Y[0])

    for y in Y:
        if sum(A[-1]) + y <= n:
            A[-1].append(y)
        else:
            A.append([y])
    return A
    
```


```python
nextfit([6, 1, 5, 2, 0, 8, 7, 3, 4, 9],10)
```




    [[6, 1], [5, 2, 0], [8], [7, 3], [4], [9]]



## First Fit Algorithm

Put each item as you come to it into the oldest (earliest opened) bin into which it fits.


```python
X = [5, 2, 0, 8, 7, 3, 4, 9, 1]

n = 10 #bin size

print(X)

A = []
Y = X

A.append([Y[0]])
Y.remove(Y[0])

for y in Y:      #work through the elements we need to put into bins from left to right
    for a in A:  #extra loop looks from left to right at existing bins and tries to fit in elements
        if sum(a) + y <= n:
            a.append(y)
            break
    else:
        A.append([y])
    print(A)
```

    [5, 2, 0, 8, 7, 3, 4, 9, 1]
    [[5, 2]]
    [[5, 2, 0]]
    [[5, 2, 0], [8]]
    [[5, 2, 0], [8], [7]]
    [[5, 2, 0, 3], [8], [7]]
    [[5, 2, 0, 3], [8], [7], [4]]
    [[5, 2, 0, 3], [8], [7], [4], [9]]
    [[5, 2, 0, 3], [8, 1], [7], [4], [9]]



```python
def firstfit(X,n):  #inputs both a list and a size of bin
    A = []
    Y = X

    A.append([Y[0]])
    Y.remove(Y[0])

    for y in Y:      #work through the elements we need to put into bins from left to right
        for a in A:  #extra loop looks from left to right at existing bins and tries to fit in elements
            if sum(a) + y <= n:
                a.append(y)
                break
        else:
            A.append([y])
    return A
    
```


```python
firstfit([5, 2, 0, 8, 7, 3, 4, 9, 1],10)
```




    [[5, 2, 0, 3], [8, 1], [7], [4], [9]]



## Worst Fit Algorithm

Put each item into the emptiest bin among those with something in them. Only start a new bin if the item does not fit into any which are already started. In the event of a tie go with the earliest bin.

A key observation is if it doesn't fit into the emptiest bin it won't fit in any existing bin so we can break the searching loop.



```python
X = [5, 2, 0, 8, 7, 3, 4, 9, 1]

n = 10 #bin size

print(X)

A = []
Y = X

A.append([Y[0]])
Y.remove(Y[0])

for y in Y:
    B = []
    for a in A:
        B.append(sum(a))
    low = min(B)        #what's the value in the emptiest bin
    for a in A:
        if sum(a) == low:   #test to see if it is one of the emptiest bins
            if sum(a) + y <= n:
                a.append(y)
            
            else:
                A.append([y])
            break
    print(A)
```

    [5, 2, 0, 8, 7, 3, 4, 9, 1]
    [[5, 2]]
    [[5, 2, 0]]
    [[5, 2, 0], [8]]
    [[5, 2, 0], [8], [7]]
    [[5, 2, 0, 3], [8], [7]]
    [[5, 2, 0, 3], [8], [7], [4]]
    [[5, 2, 0, 3], [8], [7], [4], [9]]
    [[5, 2, 0, 3], [8], [7], [4, 1], [9]]



```python
def worstfit(X,n):
    
    A = []
    Y = X

    A.append([Y[0]])
    Y.remove(Y[0])

    for y in Y:
        B = []
        for a in A:
            B.append(sum(a)) # B is a list of the sum in each bin within y loop
        low = min(B) 
        for a in A:
            if sum(a) == low:
                if sum(a) + y <= n:
                    a.append(y)

                else:
                    A.append([y])
                break
      
    return A
```


```python
worstfit([5, 2, 0, 8, 7, 3, 4, 9, 1],10)
```




    [[5, 2, 0, 3], [8], [7], [4, 1], [9]]



## Worst Fit Decreasing

A typically very efficient approach which combines putting the pieces in descending order before applying the Worst Fir algorithm.

To put in descending order I use the built-in ```sorted()``` function followed by a loop which writes the list backwards.


```python
Y = sorted([4,6,7,8,4,5,10])
Z = []
i = 1
while i <= len(Y):
    Z.append(Y[-i])
    i = i+1
print(Z)
```

    [10, 8, 7, 6, 5, 4, 4]



```python
def worstfitdecreasing(X,n):
    Y = sorted(X)
    Z = []
    i = 1
    while i <= len(Y):
        Z.append(Y[-i])
        i = i+1
    return worstfit(Z,n)
```

## Comparison

I'm not attempting to rigorously test efficiencies here, but I propose to look at 100 lists of 10 random numbers between 0 and 10, placed into bins of capacity 20 and look at the average number of bins needed by the three four approaches: ```nextfit(X,n)```; ```firstfit(X,n)```; ```worstfit(X,n)```; ```worstfitdecreasing(X,n)```.


```python
A=[] #List to store number of bins of nextfit(X,n)
B=[] #List to store number of bins of firstfit(X,n)
C=[] #List to store number of bins of worstfit(X,n)
D=[] #List to store number of bins of worstfitdecreasing(X,n)

i = 0
while i <100:
    X = random.sample(range(10), 10)
    A.append(len(nextfit(X,20)))
    B.append(len(firstfit(X,20)))
    C.append(len(worstfit(X,20)))
    D.append(len(worstfitdecreasing(X,20)))
    i = i+1

print "Bin efficiency for the nextfit algorithm:", sum(A)/100.0
print "Bin efficiency for the firstfit algorithm:", sum(B)/100.0
print "Bin efficiency for the worstfit algorithm:", sum(C)/100.0
print "Bin efficiency for the worstfitdecreasing algorithm:", sum(D)/100.0
```

    Bin efficiency for the nextfit algorithm: 5.98
    Bin efficiency for the firstfit algorithm: 2.63
    Bin efficiency for the worstfit algorithm: 2.31
    Bin efficiency for the worstfitdecreasing algorithm: 2.02


We already see the expected pattern, with ```worstfitdecreasing``` superiority beginning to emerge.