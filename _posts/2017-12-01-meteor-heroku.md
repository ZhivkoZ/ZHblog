---
layout: post
title:  "How to Run a Meteor.js Application on Heroku"
date:  2017-12-01
project: true
tag:
- Heroku
- deployment
- deploy
- Meteor.js
---

{% include toc.html %}

![Logo]({{ site.url }}/{{ site.picture }}){: .selfie}

<center>How to Run a Meteor.js Application on Heroku</center>

### What?
* How to Run a Meteor.js Application on Heroku

## Set Buildpack for Heroku Instance
{% highlight text %}
1) Run:
$ heroku create [yourappname] --stack cedar --region us --buildpack https://github.com/jordansissel/heroku-buildpack-meteor.git
Use the reliable Meteor Buildpack Horse!:
{% highlight yaml %}UPDATE: use this buildpack instead
heroku buildpacks:set https://github.com/AdmitHub/meteor-buildpack-horse.git
{% endhighlight %}
UPDATE2: use this build pack to run with iOS and android platforms added
https://github.com/Alveoli/meteor-buildpack-horse
{% endhighlight %}

## Clone the Heroku repo and cd into it:
{% highlight text %}
2)$ git clone https://git.heroku.com/[yourapp].git && cd [yourapp]
{% endhighlight %}

* Create a git instance
* Login to Heroku

{% highlight text %}
  i.e.:
git init
git add
git commit

heroku login
{% endhighlight %}   

## Create and Configure a New mLab Instance
{% highlight text %}
3) Add the MongoLab addon in the Heroku dashboard or in terminal:
$ heroku addons:create mongolab
Must have MONGO_URL configured to be the same like MONGOLAB_URI !!!!

heroku config | grep MONGODB_URI ////// Running "heroku config" will list all configuration flags set on your app ///

Next, we configure our Meteor app to use this address:

heroku config:add MONGO_URL=<MONGODB_URI value>
heroku config:add ROOT_URL=https://example.herokuapp.com

  {% endhighlight %}
## Deploying to Heroku
We must check that we can push to Heroku:

{% highlight text %}
git remote -v
Output should be:
heroku  https://git.heroku.com/example.git (fetch)
heroku  https://git.heroku.com/example.git (push)

Now we can deploy the app:

git push heroku master

{% endhighlight %}

## Navigate to your app
{% highlight text %}
 https://[yourapp].herokuapp.com/
{% endhighlight %}
## Closing Remarks
{% highlight text %}
you must have a Procfile and package.json within your meteor app directory

To set up email client on Heroku (I chose Mailgun by Mailchimp)
Make sure you set up the MAIL_URL, see http://docs.meteor.com/#/full/email

{% endhighlight %}
## About Meteor and Heroku
Meteor
Meteor is an open-source, full-stack JavaScript development platform for rapid app development. You can view the full Meteor API   [here](https://docs.meteor.com/index.html){: .btn}.

Heroku is an excellent PaaS provider for hosting your app in the cloud. Scaling your app is easy and there are plenty of add-ons to ready your app for whatever audience you’re targeting.
