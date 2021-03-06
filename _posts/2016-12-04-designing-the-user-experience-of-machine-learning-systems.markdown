---
layout: post
title: Designing the User Experience of Machine Learning Systems
date: '2016-12-04 18:31:06'
tags:
- thingslearn
- iot
- software
- analytics
---

A few months ago I submitted an abstract to a UX conference. I'm not sure if my proposal is going to be accepted, but I thought it would be worth sharing my thoughts on the user experience of Machine Learning Systems on my currently quite neglected blog.

Those who follow [@BorisAdryan](https://twitter.com/BorisAdryan) on Twitter may have heard about my [Thingmonk](http://www.thingmonk.com) talk about that very subject:
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/OUlgsle6UpM" frameborder="0" allowfullscreen></iframe>
</center>

While the [slides for my talk](http://www.slideshare.net/BorisAdryan/thingmonk-2015) are pretty self-explanatory, the following abstract delivers my motivation a bit more systematically.
<br>

### Designing the User Experience of Machine Learning Systems
Computers don't have a notion of the world around them. Nevertheless, the current generation of personal devices already attempts to hide that fact by providing context-specific information and recommendations that are based on some interpretation of previous input (e.g. search terms) and behaviour (e.g. commute patterns). At this stage, most users don't expect websites, mobile phones or tablets to give useful predictive insight. True-positive predictions (*'I see you're arriving at the cinema - would you like to see a list of movies?'*) are often met with positive surprise, false-positive predictions (*'Customers who bought this book about contraception als wanted to know about diapers'*) provoke laughter. **We usually expect to be disappointed and recommender systems to be broken - it's the reality of machine learning UX.**

With the anticipated billions of devices that make up the Internet of Things, it becomes clear that information overload is imminent. We cannot longer digest the vast amount of raw data coming off these devices; i.e. from a practical as well as a UX perspective we have to get away from looking at raw output on dashboards (the proverbial 'app for each device') to intelligent systems that can deal with this data in real-time and provide users with agglomerated context-specific information and relevant, actionable insight. Add speech: Rather than having a nagging voice remind us every minute of an impending energy crisis, we only want to interrupt a journey if it is clear that it cannot be completed without refuelling the car, and that there is a reasonably opportunity to do so nearby. A well-trained machine learning method could be used to infer such 'knowledge' from a set of arbitrary data, based on statistical considerations and properties of previously learned data.

A machine learning method may build a classifier that categorises combinations of incoming data (e.g. amount of gas, distance to target, distance to next gas station, etc) as belonging to groups (*'this is a good opportunity for refuelling'* or *'this is not a good moment to annoy the driver'*). Conceptually we can use the classifier at any time (even when it is not 'trained'), but the initial state of any machine learning system is that of ignorance, i.e. it is unclear whether or not a a prediction is true and the decision may be random. While 'on-the-fly' learning exists, **ultimately all machine learning is iterative and requires regular feedback** to clarify to the computer whether a given set of data really belongs to one or another group: **this is the training phase that makes the classifier useful, and more training and more feedback means better classifiers**.

In academic machine learning method development, as well as in applications of machine learning in the industrial R&D context, training is a widely accepted, necessary evil. **Things become tricky when machine learning and the uninitiated consumer come together.** When a user without knowledge of the underlying process is confronted with repeated confirmation requests (*'Do you agree this is a good moment to stop?'*), **the training phase can become a UX nightmare** that in the worst case makes the user avoid the system altogether, before it ever can become any good. We are already seeing websites and apps that use iterative training. Some take the confirmation strategy, but don't communicate why they're doing it. Others present even objectively bad predictions but allow the user to mark and discard these. Is voice control in respect to providing feedback to machine learning systems more or less intrusive? It seems that systematic A/B testing is required, as some communities (e.g. home automation geeks vs. professional truck drivers) may be more appealed by one or the other strategy.

While providing a metric of the reliability of a prediction is a must for engineers, **confronting consumers with p-values, false discovery rates or area-under-the-curve is a clear no go.** What is the best strategy to go about it? People of a certain age will remember how any weather forecast longer than a day into the future was just a random guess, and accepted the very fact. Nowadays, some weather websites feature a reliability score. But if an arbitrary '34% reliability' provide more ‘actionable insight’ than the sheer acceptance that predictions are random is unclear.

**Can we avoid all this trouble by creating vast training facilities for machine learning algorithms in connected products? Likely not.** Good machine learning requires lots of training data. Power comes with large numbers. However, most predictions for the Internet of Things are going to be based on the integration of data across different devices. As everyone might have a different combination of devices that should be taken into consideration, and everyone might have a different scope for using the Internet of Things (the *'What does our user want?'* -- think security, fitness, efficiency), providers of machine learning solutions cannot train their methods without the users themselves. We may want to think about large-scale simulations that draw bootstrapped ensembles of virtual devices and try to infer ‘this particular virtual user’s need’, but ultimately this will only lower the number of classes we’re trying to predict — if our features and classification itself are correct, that’s still subject to some sort of (human?) supervision.

**My personal conclusion:** Coming from the perspective of a machine learning method developer and having experienced bad UX around self-learning devices myself, I cannot provide solutions to the discourse but act as an interpreter between the fields.