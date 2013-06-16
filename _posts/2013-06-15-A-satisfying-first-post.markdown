---
layout: post
title:  "A Satisfying First Post"
date:   2013-06-15 15:47:11
categories: jekyll setup
---

Ahhh... getting this up and going feels so nice.
One thing I found is the jekyll directories will need to be in the `username.github.io` directory if you want them to be found easily by the github pages engine.  I had run `jekyll new` from inside my josephhess.github.io directory on my local repo which created a subdirectory that the pages engine wasn't seeing automatically. I just moved them up one and that solved the problem. It is really nice to run `jekyll serve` and get local checking so easily

I'm leaving the code snippet below for reference, it is part of the standard first post that jekyll gives you.

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out my [Linked-in profile][linkedin] for more info on me. You can see one of my startup projects [here][28dayhug].

[28dayhug]: http://28dayhug.com/
[linkedin]: http://www.linkedin.com/in/josephhess/
