## Part I: Elements & Building Blocks

### Elements of DDD

### Domain

We have already mentioned a couple of times the term domain but we have not stopped to define it yet.

According to Eric Evans (the creator of DDD), the domain is "a sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software"[^1].

If, for example, we are building a basic calculator app, then the domain of our application is the four basic arithmetic operations (and all the things directely related with it).

### Ubiquitious Language

The ubiquitous is a busines-centric language used by all team members as the "official" communication language. Communication between designers, developers and business people is hard. The reason behind that is: we speak different languages.

Developers talk using a language that other developers understand, same thing happens with designers, buisnes people, marketing people etc.

On a multidisciplinary and/or cross-functional team this becomes a real issue. The ubiquitous language aims to solve this problem by providing a common (ubiquitious) vocabulary that everyone knows and understand.

The ubiquitious languages is defined with the help of every team member and the domain experts. This language, just as the busines and the software, is always changing and evolving to adapt to the needs of the busines.

### Model

The model as defined by Eric Evans is "A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain."[^2]. This means that the model is not a class, a type, an interface or a datase table, but it can be a mix of those. The model aims to be as technology-agnostic as possible. The purpose of the domain is, again, not to reflect the implementation details of the technology we are using but to reflect the domain in which we are operating.

### Bounded Context

Every model has a context in which it makes sense. If we take the model outside of the context then the model will lose meaning.

Big pieces of software can (and will usually) have multiple contexts. These context can have some duplication regarding the modeling: they work with the same model. When this happens is pretty common for models to stray away from each other.

These discrepancies sometimes can be aliviated by removing duplication and unifying multiples models into a single one. This, however, is not always possible.

Many times bounded (specific) contexts cannot be unified under a single (general) context. So we end up with bounded contexts having their own models and doing a mapping between contexts when we need them to work together.

This is not only expected, but natural. Instead of fighting this phenomena is better to have a clear boundary: where a bounded context starts and when it ends; and a mapping mechanism between contexts. The ubiquitious language is the tool that allows us to define those boundaries and those mappings.

## DDD Building Blocks

As mentioned during the introduction, DDD comes with some building blocks, this building blocks are the technical foundation that will allow us to model our domain. Not all of these are used nor needed at the same time, some of those are more common on different "flavors" of DDD[^3].

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

### Domain Events

Domain events are things that have already happened inside the domain.

As we discussed earlier, entities keep track of their state an life cycle (they are aware they change), but they are not aware of the reason behind those changes.

There are multiple mechanisms to try to keep track of these changes outside of the domain model (cloud traling, logs, history changes). But these mechanisms are not optimal and rely heavily on concepts outside of the domain.

Domain events work as a log system that not only tells us what happened inside the domain, but also express why it happened. They are not the same as application events (like `file oppened`, `file closed`, `database connection stablished`, etc), application events are charged with technical implementation details, while domain events are heavily charged with domain concepts.

By representing things that happened inside the domain we can derive the current state of entities inside of the domain in the absence of data. This allows us to keep consistency in distributed systems[^eventual-consistency].

By being descriptions of things that already happened domain events cannot change (hey are immutable) but by also being descriptions of why things happened they need to have all the context necessary to interpret them. This context can include the data that changed, the timestamps of when this happened, the ids of the "affected" entities and/or the ids of the person/system responsible of the change.

### Services

Sometimes transformations that are unnatural to the domain are presented to us. Since these transformations do not make sense in the context of the domain it is convenient to extract them out into services.

Services, just like any part of our design, should have a clear name, have an intention-revealing interface (contract) and be part of our ubiquitious language.

Services are by nature "doers". They do not represent nor hold data, they just perform actions.

### Modules

Modules are logical groupings of sets of cohesive concepts. Modules can be used to tell the "story" of the system.
Modules should have a limited and tight scope. They allow low coupling by being indepndent logical groupings, and allow high cohesion by mainting all its concepts close[^close-near].

Modules are also part of the ubiquitious language, and as such, should have a meaningful and well dedfined name.

### Aggregates

Objects that have many associations with other objects have a hard time trying to keep an internal state consistent.
This is due to the nature of the relationships between internal states. One change on the internal state of an entity can trigger a change in another's internal state, and so on, and so on.

To avoid this ripple effect we must group entities and value objects into aggregates and define clear boundaries around them.

An entity will always work as the root: the entry point of the aggregate. The aggregates can only be referenced thru the root. Other objects should not have access to the internals of the aggregate.

Aggregates should always be in a consistent state, therefore, is important to define all their invariants and always enforce them.

Within the boundaries of the aggregates all the operations must be done synchronously to enforce consistency. Meanwhile, all operations outside of the aggregate can be done asynchronously.

### Repositories

Repositories allow us to access query to aggregates. We must avoid querying specific data and transformations using concepts outside of the domain (i.e sql).

We must enforce consistency by querying aggregates using repositories. Querying data transformations using other mechanisms can bypass the rules of our domain and lead to an inconsistent internal state[^garbage-in-garbage-out] and breach encapsulation. Also, by bypassing the domain and placing the query logic somewhere else we turn our rich and expresive entities and value objects into mere data containers[^anemic-domain-model].

To enforce consistency repositories must create the illusion of in data memory by serving as the global data access.

Aggregates also must define at root level methods for adding and/or removing objects within their boundaries. And selectors for data querying to avoid relying on out-of-domain concepts. When querying aggregates they should return full and consistent instances of entities/value-objects.

We should avoid having repositories that work for multiple aggregates, one repository for each aggregate.

### Factories

Factories allows us to encapsulate object assembly[^object-assembly]. This is specially useful while dealing with complex objects that rely on many relationships. Complex assembly should always fall under factorie's responsibilities and not the objects themselves. Mxising both responsibilities, assembly and creation[^assembly-vs-creation], of objects can lead to a muddy design. It is better to keep them separated. Any complex object creation should be delegated completely to factories.

Any object created thru factories should be in a valid state. Factories achieve this by always enforcing object's invariants.

Complex assembly operations can be aided by the usage of builders and other patterns[^builder-pattern].

[^1]: "a sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software" -- Domain-Driven Design Reference: Definitions and Pattern Summaries
[^2]: "A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain." -- Domain-Driven Design Reference: Definitions and Pattern Summaries
[^3]: Even though there's no "true" DDD style/flavor, there are some styles that are common. Some of these styles/flavors are diametrically opposed. The two most obvious would be a heavily OOP inspired flavor vs a heavily FP inspired flavor. Other examples are repository-based vs CQRS-based.
[^onion-architecture]: See ["The Onion Architecture: Part 1"](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/) for reference
[^open-closed-principle]: See ["Open/Closed Principle"](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle) on Wikipedia
[^hexagonal-architecture]: See ["Hexagonal Architecture"](https://alistair.cockburn.us/hexagonal-architecture/) for reference.
[^open-layers-closed-layers]: [Software Architecture Patterns](https://towardsdatascience.com/software-architecture-patterns-98043af8028) by Anuradha Wickramarachchi
[^structural-equality]: When dealing with terms of identity we must avoid structural equality at all costs. As we said, antities can have different representations, this includes having more or less fields/properties in certain points of times. Also, structural inequality becomes useless when we compare the same entity over times since entities' internal state can change.
[^external-ids]: It is pretty common to delegate the identity definition/generation to external services like databases or other persistance mechanisms.
[^eventual-consistency]: See ["Eventual Consistency"](https://en.wikipedia.org/wiki/Eventual_consistency) on Wikipedia
[^close-near]: They are close in the sense that everything is near of each other, not that they are closed to modification.
[^garbage-in-garbage-out]: See ["Garbage-in, Garbage-out"](https://en.wikipedia.org/wiki/Garbage_in,_garbage_out) on Wikipedia
[^anemic-domain-model]: See ["Anemic Doamin Model"](https://en.wikipedia.org/wiki/Anemic_domain_model) on Wikipedia
[^object-assembly]: Also known by the names of aggregation, composition and augmentation.
[^assembly-vs-creation]: Creation can also be accomplished thru factory functions. But the usage of factories for object creation is not that common in OOP languages due to widespread usage of classes and constructors.
[^builder-pattern]: See ["Builder Pattern"](https://en.wikipedia.org/wiki/Builder_pattern) on Wikpedia
