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

The model as defined by Eric Evans is "A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain."[^3]. This means that the model is not a class, a type, an interface or a datase table, but it can be a mix of those. The model aims to be as technology-agnostic as possible. The purpose of the domain is, again, not to reflect the implementation details of the technology we are using but to reflect the domain in which we are operating.

### Bounded Context

Every model has a context in which it makes sense. If we take the model outside of the context then the model will lose meaning.

Big pieces of software can (and will usually) have multiple contexts. These context can have some duplication regarding the modeling: they work with the same model. When this happens is pretty common for models to stray away from each other.

These discrepancies sometimes can be aliviated by removing duplication and unifying multiples models into a single one. This, however, is not always possible.

Many times bounded (specific) contexts cannot be unified under a single (general) context. So we end up with bounded contexts having their own models and doing a mapping between contexts when we need them to work together.

This is not only expected, but natural. Instead of fighting this phenomena is better to have a clear boundary: where a bounded context starts and when it ends; and a mapping mechanism between contexts. The ubiquitious language is the tool that allows us to define those boundaries and those mappings.

## Common practices promoted by DDD

When I first found DDD I was looking for an "architecture" to help me scale the piece of software that I was working on at the moment. DDD is more than a bunch architectural patterns and a "file structure". It's a process that enables better communication.

Because of this DDD plays really well with some practices that we could consider "standard" on the software industry

### Agile

DDD makes a strong emphasis on understanding the domain of the problem we are trying to solve first. Because of that DDD leans to avoid creating a big design up front[^big-design-up-froant]. If we are or have a strong connection with the domain experts, we cannot know everything before hand.

That's whay DDD makes an emphasys on making incremental refinements to the domain modeling and the ubiquitious language.

DDD welcomes changes: when the domain modeling changes we must update the ubiquitious language to reflect that and visce-versa.

### Continious Integration

By making use of bounded contexts DDD allows us to "partitioned" the application into smaller pieces. This helps big teams to be splitted in smaller teams and letting them work on sub-parts of the application without interfiring one with another.

By promoting Continious Integration conflicts between teams and domain modeling can be spotted and aliviated "fast".

### TDD

Because we are constantly updating the domain modeling we must have a strong mechanism that assures us that the constant changes that we make donnot break the code. TDD is that mechanism. Is a safety net that prevents us from breaking breaking existing code. But also, when we have an extensive and well defined test suite introducing new changes to the system becomes trivial.

Making the benefits of TDD twofold: not only we have a safety net, but also a mechanism that makes the software easy to change.

### Refactoring

We have described earlier the process of updating the domain modeling and the ubiquitous language as refining. The technical term for this is refactoring. When we discover new information or new insights about the domain we are driven to update the domain modeling to reflect those changes by refactoring the existing models.

Refactoring not only goes hand-in-hand with DDD, but also with TDD, by being the tool that facilitate us updating the code without breaking existing behavior.

Refactoring, promoted by DDD and supported by TDD, makes the process of updating and refining the code base something common. In other words, the quality of the code should be always improving[^refactoring].

## DDD Building Blocks

As mentioned during the introduction, DDD comes with some building blocks, this building blocks are the technical foundation that will allow us to model our domain. Not all of these are used nor needed at the same time, some of those are more common on different "flavors" of DDD[^4].

- Layered Architecture
- Entities
- Value Objects
- Domain Events
- Services
- Modules
- Aggregates
- Repositories
- Factories

We'll favor an FP inspired flavor on the following examples and use cases.

### Layered Architecture

Early versions of DDD relied heavily on OOP design patterns and a layered architecture[^onion-architecture]. This architecture is composed of three layers:

- domain
- application
- infrastructure.

Domain is the inner-most layer, followed by the application layer and finally with the infrastructure layer as the outer-most layer.

By choosing a layered architecture we can ensure that our modeling is only responsible on how to express the domain. The models should not worry on how they are presented (User Interfaces) nor how they are store (Databases). That's why they are in the inner most layer. The models are ignorant to eveyrhing else outside of the domain.

The application layer contains all the business logic of our application. The application layer can only extend the already defined rules and laws that govern the domain layer[^open-closed-principle].

Lastly, the infrastructure layer is in charge of the communication with the outside world[^hexagonal-architecture]. By placing the infrastructure layer as the most-external layer the domain and application are ignorant on the "less important" implementation details. The inner layers don not know if the application is driven by a http socket, a gui, a RPC or any other IO device. That includes the persistence mechanisms (databases). That's why we usually refer to DDD as a persitence-ignorante architecture.

The key point behind a layered architecture is isolation and decoupling. Inner are cohesive and only depend on themselves and inner layers, but not on outer layers.

Even though DDD favors a three layer approach there's no restriction on adding more layers when needed. But DDD recommends the use of closed-layers instead of open-layers[^open-layers-closed-layers].

### Entities

Some objects have a lifecycle: they go thru a stream of internal transformation. In order to know if two objects are the same object we need to develop a mechanism that allows us to identifying them. In other words, they need to have an identity.

This is the property that differentiate entities from other objects. By having an identity we can take the same object in two different points of time know they are the same entity.

This also applies with different representations: we can change the shape or form of the object and by comparing the identity we can still know they are the same object. The inverse is also applicable: two entities are different if they don't hold the same identity.

We must have a clear and well defined mechanism iniside our model to stablish and differentiate identity[^structural-equality]. The implementation details is not important as long as they are consistant[^external-ids].

A weak or unclear identity mechanism will most likely lead to data corruption: updating or referencing the wrong entity.

Entities, just like any other object of our model, is a domain concept. And as such entities have well defined attributes, relationships and actions.

### Value Objects

Value objects are also domain concepts and are charged with significant meaning, but instead of being their own thing they usually represent a characteristic or a computation of something else.

By nature of being property or computation descriptors value objects are immutable and side-effect. They don't keep track of their internal state changes, due to that value objects don't need to have an identity mechanism. They are interchangeable with one and another.

It is common for entities to be composed partially or completely by value objects.

[^1]: When we say piece we do not specifically mean "small".
[^2]: "a sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software" -- Domain-Driven Design Reference: Definitions and Pattern Summaries
[^3]: "A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain." -- Domain-Driven Design Reference: Definitions and Pattern Summaries
[^open-closed-principle]: See ["Open/Closed Principle"](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle) on Wikipedia
[^4]: Even though there's no "true" DDD style/flavor, there are some styles that are common. Some of these styles/flavors are diametrically opposed. The two most obvious would be a heavily OOP inspired flavor vs a heavily FP inspired flavor. Other examples are repository-based vs CQRS-based.
[^hexagonal-architecture]: See ["Hexagonal Architecture"](https://alistair.cockburn.us/hexagonal-architecture/) for reference.
[^big-design-up-froant]: See [Big Desing Up Front](https://en.wikipedia.org/wiki/Big_Design_Up_Front) on Wikipedia
[^onion-architecture]: See ["The Onion Architecture: Part 1"](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/) for reference
[^refactoring]: DDD promotes a style of refactoring that should always aim to strengthten the model, not to weaken it. In other words: we should not refactor just for the sake of, but with the clear intention in mind of making the model more accurate.
[^open-layers-closed-layers]: [Software Architecture Patterns](https://towardsdatascience.com/software-architecture-patterns-98043af8028) by Anuradha Wickramarachchi
[^structural-equality]: When dealing with terms of identity we must avoid structural equality at all costs. As we said, antities can have different representations, this includes having more or less fields/properties in certain points of times. Also, structural inequality becomes useless when we compare the same entity over times since entities' internal state can change.
[^external-ids]: It is pretty common to delegate the identity definition/generation to external services like databases or other persistance mechanisms.
