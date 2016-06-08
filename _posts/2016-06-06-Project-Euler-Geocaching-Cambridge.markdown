---
layout: post
title:  "Project Euler Geocaching Cambridge"
date:   2016-06-06 20:19:28 +0100
categories: jekyll update
---

A couple of years ago I used the [Project:Euler](https://projecteuler.net) challenges as a stimulus/introduction to`Python`. They were good at teaching the basics, but the motivation camr from solving quite geeky maths challenges. I discovered last summer that these had been used as the basis for a series of "mystery" [Geocaches](https://www.geocaching.com/play) around Cambridge, UK. 

The cool idea is that these [special GeoCaches](https://www.geocaching.com/bookmarks/view.aspx?guid=efc9ca64-3d99-4d32-b2ef-47699f7b7651) require you to write pretty much the same code as for the Euler Challenges, apply the code to some specific values which return a number which is then used to generate co-ordinates (a checker is included on the site to avoid wild goose chases). When I set these as homework, the submission was just asking for a photo of the student with the GeoCache!

Let's take a look at the first Project:Euler challenge.

# Multiples of 3 and 5 - [Problem 1](https://projecteuler.net/problem=1)

*If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9.*

*The sum of these multiples is 23.*

*Find the sum of all the multiples of 3 or 5 below 1000.*

We might approach the problem using `Swift` code as follows (using a `Playground` in `XCode`):

{% highlight swift %}

var sum=0

for n in 1...1000{
    if n%3==0{sum = sum+n}
    else if n%5==0{sum = sum+n}
}

print(sum)

#=> prints '234168' to STDOUT.

{% endhighlight %}


The first Project:Euler inspired Geocahe  introduced as follows:

*If we list all the natural numbers below 10 that are divisible by 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.*

*Define f(n) as the sum of the multiples of 3 and 5 which are less than n. Thus we can write:* 

*f(10) = 23.*

*Then N = f(4720) + f(240) + f(77),*

*and E = f(175) + f(10).*

{% highlight swift %}

func f(n:Int) -> Int {
    let m = n-1
    var sum=0
    for n in 1...m{
        if n%3==0{sum = sum+n}
        else if n%5==0{sum = sum+n}
    }
    return sum
}

let N = f(4720) + f(240) + f(77)

let E = f(175) + f(10)

print("N =", N)
print("E =", E)

#=> prints 'N = 5212178, E = 7141' to STDOUT.

{% endhighlight %}
This translates as the the co-ordinates N 52&deg;12.178 and E 00&deg;07.141. Which we can enter into the Geochecker for confirmation and discover a location near my PhD advisor's rooms in Corpus!

![alt text](/assets/GCCC.jpg "I like to Cache!")

