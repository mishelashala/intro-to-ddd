# Domain-Driven Desing (DDD)

## Introduction

DDD is a software design process that enables developers to transform complex pieces[^1] of software into managable one thru the use of a declarative domain modeling and design.

A declarative design is that which reflects the domain of the problem we are trying to solve, instead of reflecting the technical implementation details of the solution.

Declarative design are (until certain degree) technology agnostic. Instead of putting all the emphasis on the technology we are using to solve the problem, we put all the emphasis on the problem itself.

We achieve this thru the usage of a busines-centric language called the ubiquitous language. Instead of using technical jargon to communicate with teams we use a language that reflects the domain we are trying to solve.

The ubiquitious language is shared language stablished by the team members to describre the domain. This language, just like any piece of software, is in constant refinement and evolution.

DDD is all about communication; not about architecture, technical decisions, design patterns nor programming languages. This does nott mean that these things are not important, it just means these are secondary.

DDD comes with some technical building blocks and a suggested architecture, but as anything in software, these pre-made decisions are not mandatory nor final. These building blocks and architecture are just a suggested starting point. It is almost certain that most pieces of software will stray away from these pre-made suggestions over time due to the evolutionary nature of software. DDD is an agile and evolutionary process, so, this is not only expected, but also heavily promoted by DDD.

## Basic Definitions

### Domain

We have already mentioned a couple of times the term domain but we have not stopped to define it yet.

According to Eric Evans (the creator of DDD), the domain is "a sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software"[^2].

If, for example, we are building a basic calculator app, then the domain of our application is the four basic arithmetic operations (and all the things directely related with it).

### Ubiquitious Language

The ubiquitous is a busines-centric language used by all team members as the "official" communication language. Communication between designers, developers and business people is hard. The reason behind that is: we speak different languages.

Developers talk using a language that other developers understand, same thing happens with designers, buisnes people, marketing people etc.

On a multidisciplinary and/or cross-functional team this becomes a real issue. The ubiquitous language aims to solve this problem by providing a common (ubiquitious) vocabulary that everyone knows and understand.

The ubiquitious languages is defined with the help of every team member and the domain experts. This language, just as the busines and the software, is always changing and evolving to adapt to the needs of the busines.

### Model

The model as defined by Eric Evans is "A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain."[^3]. This means that the model is not a class, a type, an interface or a datase table, but a mix of one or many of those. The model aims to be as technology-agnostic as possible. The purpose of the domain is, again, not to reflect the implementation details of the technology we are using but to reflect the domain in which we are operating.

## Architectural Patterns

## Building Blocks

As mentioned during the introduction, DDD comes with some building blocks, this building blocks are the technical foundation that will allow us to model our domain. Not all of these are used nor needed at the same time, some of those are more common on different "flavors" of DDD[^4].

- Entities
- Value Objects
- Domain Services
- Aggregates
- Repositories
- Mappers
- Factories
- Domain Events
- Application Services

We'll favor a FP flavor on the following examples and use cases.

### Architectural Decisions

[^1]: When we say piece we do not specifically mean "small".
[^2]: "a sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software" -- Domain-Driven Design Reference: Definitions and Pattern Summaries
[^3]: "A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain." -- Domain-Driven Design Reference: Definitions and Pattern Summaries
[^4]: Even though there's no "true" DDD style/flavor, there are some styles that are common. Some of these styles/flavors are diametrically opposed. The two most obvious would be a heavily OOP inspired flavor vs a heavily FP inspired flavor. Other examples are repository-based vs CQRS-based.
