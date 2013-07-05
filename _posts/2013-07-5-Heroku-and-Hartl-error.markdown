---
layout: post
title:  "Heroku and Hartl error you might have"
date:   2013-07-5 15:47:11
categories: rails tutorial
---

if you end up seeing this error:
{% highlight ruby %}
!     Push rejected, no Cedar-supported app detected
{% endhighlight %}
 among the many things it could be - it might be as simple as you need to initialize a new repository specifically for the heroku app you want to deploy.
 this may seem patently obvious but since i was deep in an already intialized repo it didn't occur to me that that could be the issue and looked over all sorts of other stuff before realizing that might be my prob.

 since i was in a subfolder of a more general repo i use for schoolwork heroku was looking at the git file for the whole repo and couldn't  see the folder as a rails app - since it wasn't :/

 also, you will need to commit any changes you make to the gemfile so that heroku can see them - it's not just enough to run bundle install.

so when you change sqlite3 to development and make pg production remember to commit the changes in git :)


