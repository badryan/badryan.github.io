---
layout: post
title: Deploying a website on IBM Bluemix
date: '2014-08-11 14:26:55'
tags:
- thingslearn
- software
---

![](/content/images/2015/09/thingslearnweb.png)
As I shared a few weeks ago, I’ve started a small [company](http://www.thingslearn.com) around my Internet-of-Things activities. This is entirely based on my personal skills and interests, and therefore it felt inappropriate to host the website [www.thingslearn.com](http://www.thingslearn.com) on a computer “at work” (the University). Instead I installed Apache on my home-automation Raspberry Pi and hosted the site “from home” for a while. While that’s certainly a viable option as long as *thingslearn* isn’t too popular, as IT professional I obviously think a lot about scalability.

One of my students had previously deployed a web service to [heroku](https://www.heroku.com), but back then I didn’t even realise that Platform-as-a-Service (PaaS) is a thing. To suggest a currently often used analogy: PaaS relates to computing in a way that a restaurant dinner relates to food shopping, cooking, serving, eating and washing up. With PaaS, all the hardware and software infrastructure are provided, the user only has to select the appropriate solution from the vendor and is done with (hopefully) minimal configuration. And if your user base is growing, you just order another plate of pizza; if there’s not enough space around the table, if the kitchen is busy and if there are no more tomatoes — not your problem: The PaaS vendor will make it happen. (For a price, of course).

One PaaS offering comes from IBM as has seen General Availability last month. That’s [Bluemix](http://www.bluemix.net). And here I’m going to show how I got the [thingslearn website](http://thingslearn.mybluemix.net) onto Bluemix.

You typically start on Bluemix with a “Boilerplate” from the “Catalog”. Here you can find e.g. the Java Web Starter or the Node JS Web Starter… …but hold on, no Apache or PHP. Now that was a problem because while mostly being HTML5, *thingslearn* uses a few lines of PHP to collect email addresses for a newsletter. Fortunately, Bluemix just as heroku are based on [Cloud Foundry](http://cloudfoundry.org/index.html), which in the most simple terms could be described as a high-level operating system for PaaS (in fact it sits on top of the OS, and CF can be installed on many different platforms; and if I understand it correctly, CF does most of the software side of PaaS scaling). New applications for Cloud Foundry can be installed in the form of [buildpacks](http://docs.cloudfoundry.org/buildpacks/). My search for “apache php buildpack” brought me to this project on Github: [cf-php-build-pack](https://github.com/dmikusa-pivotal/cf-php-build-pack).

What I really like about buildpacks and the 30-second-tutorial on the Github page is that it uses the command line, and leaves much of the fancy but in my opinion too complex GUI of Bluemix behind. To implement any changes in your Bluemix area, you will need to install the [cf Command Line Interface](http://docs.cloudfoundry.org/devguide/installcf/) (CLI, or ‘cf’ in any syntax). (**THAT’S SORT OF STEP 1**).

As I wasn’t quite sure what exactly is needed to create a website, and rather than creating a file *index.php* with no other content but “<?php phpinfo() ?>”, I decided to *git clone* the recommended example applicationÂ [cf-ex-php-info](https://github.com/dmikusa-pivotal/cf-ex-php-info) (**STEP 2**), which comes with a couple of useful files, for example *manifest.yml* that contains most of the configuration for your project.

Not only does the manifest tell CF which buildpack you’d like to include, it also let’s you specific the name, host name and memory limits of your application. For example, with *host: willibob*, the URL for your project becomes *willibob.mybluemix.net*. (So, **STEP3**, edit your *manifest.yml*).

I then instructed CF to work with Bluemix (*cf api https://api.ng.bluemix.net*), log into my Bluemix account (*cf login*) and then the most important of all: ‘*cf push*‘ to upload your files and install the buildpack on the Bluemix server. (These are all **STEP4**). After a perceived eternity, that processes finished and my mini PHP-based website was up and running.

**Wait. That’s wasn’t the goal.** We wanted to get *thingslearn* online. Now I didn’t understand the inner workings of the buildpack nor CF, but I recognise a ***htdocs* directory** when I see one. In the case of the cf-ex-php-info example, the htdocs file contained a *index.php* as well as a few other files for display. I simply copied all of my directory structure from *htdocs* on my Raspberry Pi server to the htdocs directory in the *cf-ex-…* project directory, and issued a ‘*cf push*‘. Magically, my next visit to willibob showed the all-familiar *thingslearn* website. (Call that **STEP5** if you want).

<span style="text-decoration: underline;"><span style="color: #000000;">**The really difficult bit…**</span></span>

**Adjusting the PHP.** Now so far that’s all been relatively easy. Unfortunately, my PHP code that takes care of soliciting visitor emails didn’t work as desired. The server is supposed to inform me via email about any new registrations. However, [‘*sendmail*‘ is not available on Bluemix](https://developer.ibm.com/answers/questions/20048/sendmail-on-bluemix-sending-from-web-form-cf-php-apache-buildpack/?community=bluemix) (as, strictly speaking, we’re not dealing with a Unix system here).

[SendGrid](http://sendgrid.com) is a “Service” within Bluemix and takes care of most email needs. I created that service through the Bluemix GUI using their default parameters (using the SendGrid Dashboard). To make the service known to the application, I also used the GUI to “bind” the service to the app. The details about the service can be read from an environment variable called VCAP_SERVICES, and thanks to some generous code examples in the Developer Forum I learned the [syntax to inform PHP about SendGrid](https://developer.ibm.com/answers/questions/20566/sendgrid-service-in-php-application/?community=bluemix). A further call for help in the forum guided me to a code generator on SendGrid and the formulation of [some PHP code, as shown here](https://developer.ibm.com/answers/questions/22107/seeking-another-php-sendgrid-example/?community=bluemix). (**STEP6**).

I was new to PHP and its dependency management. Fortunately, I stumbled over [composer](https://getcomposer.org) (and here’s a nice summary [how to install it under Linux/OS X](https://getcomposer.org/download/)). With that, adding the SendGrid PHP API was pretty straightforward as described under Installation on [sendgrid/smtpapi-php](https://github.com/sendgrid/smtpapi-php). Composer installed a directory *vendor* within my *htdocs* directory, and with the next *‘cf push*‘ they were all happily exported to Bluemix.

**This wasn’t necessarily easy and as clear as it could have been, but I’m nevertheless quite pleased that I managed to install a web server on a PaaS.**
