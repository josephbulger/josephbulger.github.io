---
author: jbulger
comments: true
date: 2011-9-06 12:00:10
layout: post
slug: solid-principles-liskov-substitution-principle
title: 'SOLID Principles: Liskov Substitution Principle'
wordpress_id: 697
categories:
- Programming
tags:
- lsp
- SOLID
- solid-series
---

Liskov Substitution Principle, or LSP, is actually a very simple concept to understand in a strongly typed language. In languages like C#, or VB.NET, LSP often gets taken for granted, but I've seen cases where even in strongly typed languages you can violate LSP.

<!-- more -->Simply put, LSP means that for a given base class, you should be able to substitute derived classes in it's place, and the behavior or the expectation of that behavior should not change. Take for example a Shape:

[gist id=1188522 file=Shape.cs]

The point of this class is to define something which has the ability to give us it's area back. Something like a Square

[gist id=1188522 file=Square.cs]

or a Circle

[gist id=1188522 file=Circle.cs]

would have the means to give us this information.

However, something like a Line

[gist id=1188522 file=Line.cs]

would not be able to give us it's area, because it doesn't have an area. In fact, it's not even a Shape to begin with. It seems odd that I would use this as an example, but the simplicity of the example shows exactly how LSP gets violated in practice. All too often I'll see code where a class is deriving from another class, even though it's shouldn't be. At the core of the issue is usually that it was never meant to _**be**_ the thing it was deriving from in the first place.

A full running example of utilizing LSP can be found on this [video from dime casts](http://dimecasts.net/Content/WatchEpisode/92).
