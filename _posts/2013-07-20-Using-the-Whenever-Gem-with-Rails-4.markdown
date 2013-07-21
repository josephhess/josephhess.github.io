---
layout: post
title:  "Using the Whenever Gem with Rails 4"
date:   2013-07-20 15:47:11
categories: Rails Gems Scheduling
---

I was working on the payment side of my subscription site this week and needed to run daily charges on a schedule. I came across the Whenever gem which seemed just right but wasn't documented as well as could be hoped.  This post needs to be expanded and improved but can get you to a minimum working state!

To use the whenever task scheduling gem in your rails app you will want to add the gem to your gemfile and bundle first:

`gem 'whenever', :require => false`

Then from the command line in the root directory of your app type `wheneverize .` (I just assume you want to be in root but will need to check later) This will create a config/schedule.rb file for you with some example code in it.
This will be one of two interaction points for the app along with the command line.

Once you have created a task in this file you will update the cron from the command line


When you have your schedule.rb file created and filled with your task code enter at the command line 
`whenever -i project_name`(put your project identifier here, for example, the name of the rails project)
	 this is equivalent to: `whenever --update-crontab project_name`

	 you can then use `crontab -l` to look at the scripts added to cron and see thier associations

	 `whenever -c` is the equivalent of `whenever --clear-crontab`
	 	with this you will want to use the association keyword you initially setup the cron job with as in 
	 		`whenever -c project_name` or `whenever --clear-crontab project_name`

	use `whenever --help` if you can't remember what the commands are.

a quick test to see what issues you might be having is to grab the code from the `crontab -l`output and run it from the command line and see what if any errors you get. Just copy all the code for the individual task from /bin/bash....to the end and paste it at the command line.

You can also log your whenever's with-  `set :output, 'log/cron_log.log'` and create a cron_log.log file in our Rails log directory. I just used a puts statement which was added to the log file upon successful whenever calls.

A big gotcha is if you are working with rails 4 he hasn't implemented the patch to check for rails 4 yet.
This means you will get an error if you try and run it since it will be using script/runner instead of rails runner.
This means you will need to add a custom job runner as in:
	`job_type :runner, "cd :path && bin/rails runner -e :environment ':task' :output"`

The default environment is production so if you are in development mode you can add `:environment => :development` to your runner call to get it working.

all of this together resulted in the code below as a test for me and it was working great. It just cost me a couple hours worth of searching and trying things :)

in config/schedule.rb:
{%highlight ruby %}
set :output, 'log/cron_log.log'
job_type :runner, "cd :path && bin/rails runner -e :environment ':task' :output"


every 2.minutes do
  runner "Charge.charge_machine", :environment => :development
end
{% endhighlight %}
