---
author: joseph
comments: false
date: 2011-10-13 08:00:32
layout: post
slug: mental-floss-the-problem-with-my-circle-is
title: 'Mental Floss: The problem with my Circle is...'
wordpress_id: 777
categories: [mental floss, solid]
---

that I'm exposing too many details to the user of my code. The developer has to know intimate details about how to set up both the Ellipse and the Circle in order to calculate their areas effectively. In one case, the Ellipse, the runner has to know to set the major and minor axes, while for the Circle, they have know to set the Radius.

<!-- more -->The underlying problem here is simple, actually. The real issue stems from the fact that the Ellipse (and by proxy the Circle) was designed as a Hybrid object. As I've said before, and [others before me](http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882), Hybrid objects are evil. To fix this, we need to either make these classes Data Structures, or make them Objects. Since the whole point of the code is to calculate the area, I say we have to make them Objects.

To do that, I made the following changes to Ellipse:

{% gist 1279017 GoodEllipse.cs %}

Notice how MajorAxis and MinorAxis can still be extended via a subclass if need be, but they are **only** accessible from sub classes now, not from the outside world. This removes the class's Data Structure flavor and make it's a pure Object. It also has a great side benefit. Now a user can only create an Ellipse by supplying the major and minor values when the Ellipse is created. This logically makes sense because an Ellipse can't exist without it's major and minor axes.

So how does this effect the Circle now? This is how I changed the Circle:

{% gist 1279017 GoodCircle.cs %}

A lot of code has been removed. It almost seems like I've cheated somewhere, doesn't it? Well, now that Ellipse is acting as a pure Object, the only thing Circle needs to do is to explain why it's "special". As we noted before, a Circle is special because it has a Radius. In other words, it's major and minor axes have the same length. So the Circle class simply explains that relationship, and you're done. The area calculation doesn't need to be modified because the real difference was showing how the radius is related to the major and minor axes.

Now the runner is forced to use the classes in a way that prevents them from being used in inappropriate ways:

{% gist 1279017 GoodRunner.cs %}
