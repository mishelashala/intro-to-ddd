# WIP: Introduction to Domain-Driven Desing (DDD)

## Introduction

DDD is a software design process that enables developers to transform complex pieces[^1] of software into managable one thru the use of a declarative domain modeling and design.

A declarative design is that which reflects the domain of the problem we are trying to solve, instead of reflecting the technical implementation details of the solution.

Declarative design is (until certain degree) technology agnostic. Instead of putting all the emphasis on the technology we are using to solve the problem, we put all the emphasis on the problem itself.

We achieve this thru the usage of a busines-centric language called the ubiquitous language. Instead of using technical jargon to communicate with teams we use a language that reflects the domain we are trying to solve.

The ubiquitious language is shared language stablished by the team members to describre the domain. This language, just like any piece of software, is in constant refinement and evolution.

DDD is all about communication; not about architecture, technical decisions, design patterns nor programming languages. This does nott mean that these things are not important, it just means these are secondary.

DDD comes with some technical building blocks and a suggested architecture, but as anything in software, these pre-made decisions are not mandatory nor final. These building blocks and architecture are just a suggested starting point. It is almost certain that most pieces of software will stray away from these pre-made suggestions over time due to the evolutionary nature of software. DDD is an agile and evolutionary process, so, this is not only expected, but also heavily promoted by DDD.

## Three Parts

DDD is not only about code and "architecture", it also about communcation, team structure and strategic design. We are gonna follow a three part approach for this introduction: elements & building blocks, supple design and strategy design.

The first part "Elements & Building blocks" provides desfinitions on terms such as domain, ubiqutious language, etc. There's a distintion subtle disctintion between an element and a building block. An element is a part of DDD that often is not technology related, elements are abstract at code level. That doesn't mean we cant - or won't - have concrete representations of the elements at all, we'll just use a different medium.

The second part is what DDD calls "supple design". A design that is declarative, self explanatory and playful. When we say playful we mean the design incite developers to "play" with it. Instead of turning them down and scare them away, supple design welcomes them, making the process of working with the code base a joy and not torture.

The third part "Strategic Design" is about communcation and team structure. In large projects it is common - and useful - to split projects into subsystems and assign teams to them. This split can create some relationships between teams, and as such, create relationships, dependencies and communication channels between them.

## Who is this introduction for

Me, some close friends, and perhaps some internet strangers.

I've been researching and using DDD for more than a year by the time I'm writing this (June 2022). I was just looking for an "architecture" to solve all my problems and I suddenly remembered the Big Blue Book (Domain-Driven Design: Tackling Complexity in the Heart of Software). Book that, by the way, I started reading circa 2018 and never finished.

So I gave it a second chance and it basically threw me into a rabbit hole from which until this date I've not been able to scape completely.

DDD is hard to learn, not because of the lack of resources, but for the amount of concepts you have to learn and master. And as almost everything in software you have to pratice it with real life projects. So I went ahead and refactored an entire real-life project I was working on to make it more DDD-ish. It took me about two (2) months of work just to have everything in the three (3) little boxes (application, domain, infrastructure).

But I was not satisfied with the end result. Not only it did not feel natural, but it was also causing some problems. Problems that were not inherent to DDD, but to my lack of mastery. So I went ahead and started researching more, and subsequentely refactoring more. Until this date I'm still researching and refactoring, but at this point I think I have a good grasp of what DDD looks like in the real life.

At certain point I realized I was not able to explain what DDD was about. Is not only about architecture, code, language, communication and teams. Is a mix of those and many other things.

So I decided to write this introduction. This introduction is the byproduct of the collection of notes that I've gathered for the last couple of months about DDD. It is also my way to explaining what DDD is about, not only to myself, but to others.

![My Collection of Notes](https://user-images.githubusercontent.com/5624153/173580689-efe72819-4ae8-4de5-8a99-ed338982b55d.jpeg)

I'm primarely writing this for my self - and some close friends - but I hope some other people find this useful.

[^1]: When we say piece we do not specifically mean "small".
