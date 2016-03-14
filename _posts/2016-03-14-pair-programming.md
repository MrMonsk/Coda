---
layout:     post
title:      "Pair Programming"
subtitle:   "My experiences so far."
date:       2016-03-14
author:     "Yowon Yoon"
header-img: "img/bag-and-hands.jpg"
---

Working alone has always come quite naturally to me. Especially with the amazing resources available just a few searches away online, the ability to work on something without having to compensate for another person has been more enjoyable. Additionally, when I am working on something while also learning that something, the potential embarrassment of appearing lost or slow-minded is averted by lone-wolfing. 

As I learn to become a better developer however, I’ve quickly realized that new frameworks, languages, and practices are being created faster than my ability to master just one. With all the information that is out there, it is sometimes hard to discern the best way to approach solving a problem. Pair programming becomes incredibly useful in these scenarios, be it with mentors or peers. I’ve pair programmed with coding mentors many times now, and simply being able to hear and see the thought process of someone who is already an adept programmer accelerates my internalization of a particular syntax or approach to writing an algorithm. One of the downsides of pair programming with someone far beyond my own current capabilities is that it hinges somewhat on the patience of the more experienced coder, and sometimes concepts that the more experienced coder finds intuitive may be glossed over. 
> In these pair programming instances, both of us are still relatively new web developers, so we are constantly trying to remember or look up how to implement x with y syntax. The differences in our abilities to discern what is necessary from all the information available is where I think the internalization process starts.

Recently while working on several group projects, I’ve had the opportunity to pair program with peers who are closer to my level of programming expertise. Intuitively, I thought that the coding process would be slower, but I’ve found the opposite to be the case. There’s something about being forced to talk aloud to another person that clarifies what one is trying to attempt, and also pressures one to be able to communicate an idea to another person. Just yesterday I worked on a couple of simple problems with [Ethan Siegel](https://medium.com/@ethsiegel).

For the sake of brevity, I’ll focus on one of them: 

Given two arrays of integers, we needed to return the common elements. In this session, we both agreed to not enable syntax highlighting or auto-completion in our text-editor, as well as refrain from looking up any documentation to really force us to think the problem through. We took turns coming up with a possible solution (neither of which is probably the best answer) and I learned so much from just hearing another person’s thought process. 

My initial thought was to combine the two arrays together into a single large array, call the `.uniq` method on it, then compare either of the original arrays to the larger one. If there were any that matched, push those elements into a (fourth) array, and this would be returned as the “common elements”. 

Ethan on the other hand, thought of a solution where we could directly compare the two input arrays, using the array indices to compare whether `array1[0] == array2[0]`, etc. 

We started writing out the Ruby for each of these solutions, and realized that both took a few too many steps to really get working. In my proposal, there would’ve had to have been a nested loop, which seemed overly complex for such a simple problem, and in Ethan’s proposal, we would’ve also had to have accounted for the fact that the input arrays might be unordered or of different length, so directly comparing indices would require a lot more definition.

After kind of going through these possible but tedious proposals, we both remembered that Ruby has an `include?` method that would simplify our code significantly:

{% highlight ruby %}
def common_elements(array1, array2)
  common = []
  array1.each do |val|
    if array2.include? val
      common << val
    end
  end
  common
end
{% endhighlight %}

Obviously this is a super simple problem, but the exercise of cutting ourselves off from Ruby documentation or other examples online really helped ingrain this idea of thinking out several scenarios that would all work, then finding a more elegant solution (Ruby has the & operator available for arrays => `common = array1 & array2`).

Another example where I have found pair programming incredibly useful and educational, was when I was working with [Sean Lovinger](https://smlovinger.wordpress.com/) on coding our Chess app (link to orionchess). We coded a lot together over the eight-week timeline given to our group, and working through some of the harder logic of valid_moves or something as simple as drawing a chessboard with a table (rows/cells) over individual divs to use fewer lines of code only really happened because our shared eagerness to code together and not be afraid of looking stupid in front of the other person. Simply having someone in a similar boat as me was amazingly helpful, even something simple like: “Hey, I found this StackOverflow post that’s sort of related to what we’re trying to implement” and the other person responding “Yeah, I found that too, I particularly found x-person’s response super applicable.” 

Overall, I’m extremely satisfied with my exposure to pair programming so far, and especially working with someone who is around my skill level. It can be somewhat nerve-wracking at first, but the end benefit of having a more localized context to what I’m learning helps everything just stick in my head, and is totally worth the initial 5 minutes of awkwardness.
