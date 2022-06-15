# Supple Design

A supple design has two characteristics: is not considered a legacy system and developers find "pleasure" working with it.

Michael Feathers in his book "Working Effectevely with Legacy Code" defines legacy code simply as "code without tests". This definition is small, but it has a lot of nuance. There's another definition of legacy system: an old and complex system.

This definitions are not mutually exclusive, but complementary. A system with time becomes "old", but a system without tests become harder to change. When that happens the process of refactoring becomes a burden. By not being able to refactor complexity starts to pile up until it becomes almos imposible to work with the system.

A legacy system is the complete opposite of a supple design. A supple design invites developers to work with it and to make changes. By doing so, when the opportunity to simplify logic or refactoring arises it does not become a burden. Allowing the system to always be up to date and making the process of changing the model easier by reducing the cost of change. Thus generating a cycle of grace that fomments further richness, ease of work and change.

A supple design can only be achieved when the team has a deep understanding of the domain. But that does not suffice. The team must also do a concious effor to have a clear and well defined model.

By following certain patterns and rules a supple design makes its behavior obvious to developers. The behavior is "obvious" when it follows naturally the rules of the domain.

## Intention-Reveiling Interfaces

An intention-reveiling interface is achieved when every element of our model has a descriptive and meaningful name. In other words: things do what they say they do, nothing more, nothing less.

These names must always keep encapsulation intact. They not reveal implementation details -the how-, instead the focus on the task at hand -the what-. Intention-reveiling interfaces are declarative by nature.

## Side-Effect-Free Functions

Object composition, function composition or any other kind becomes hard when we don't have side-effect-free functions. Side effects make composition, specially of computations, hard to predict and understand.

Side-effect-free functions have an interesting effect over abstractions and behaviors. First, it makes abstractions predictable, and second behavior consistent. In other words, abstractions do what they say they do, and behaviors don't hold any nasty surprises.

We must favor side-effect-free functions in our systems as much as possible. One thing to note on this is that software without side-effect-free functions is impossible. A system without side-effects is impossible to reach. It behaves like a black box: nothing goes in and nothing goes out.

The idea here is not to eliminate side=effects completely, but to have them under control.

One strategy to use when we encounter operations that produce side-effects is to seggregate these operations into commands. To do this we can follow the command-query seggregation principle.

## Assertios

Assertions help us define post-operation conditions and invariantes on aggregates. Assertions help us create -and enforce- contracts for services and entites.

Every aggregate should define post-operation conditions and invariants to check the validity of the aggregate's internal state.

Instead of reinventing the wheel we can use the features that some programming languages already provide to state assertions.

Assertions can be designed and enforced thru the use of techniques such as TDD and unit testing.

Models should stay coherent and consistent all the time. They must have no contraditions in their internal state under no circunstance. Assertions are a great way to keep our models always as such.

## Stand Alone Classes

During the process of software design low coupling should always be a top priority. Clases should always aim to be self-sufficient. Classes should not rely on concepts outside of themselves and be -as much as possible- understandable without the knowledge of the entire context in which they are contained.

## Closure of Operations

To define what closure of operation is, first, we must define what an endomorphism is. In simple terms, an endomorphism is an operation that goes from itself to itself. In other words, an operation that always produces the same result type as the input type. Closure of Operations just means that an operation is an endomorphism.

When possible we must define -and favor- operations as, or at least that behave as, endomorphims.

One of the benefit of closure of operations is that they provide an interface -a contract- without the need of external dependencies. These interfaces have everything they need in theirselves to operate.

Value objects are, generally speaking, the result of operations. Making them the best candidate for closure of operations.

The same cannot be said about entities. Entities are not the result of operations, therefore is uncommon to see the use of closure of operations with entities.

## Declarative Design

The opposite of declarative design is procedural code. Some of the problems with procedural code are the lack of rigor, code duplication and de abundance of boiler plate.

Procedular codes most of the times focues on _how_ we do things, and mostly ignores _what_ we are doing. This makes procedural code lack meaning. It bears no meaningful significance nor relationship with our model.

Declarative code, in the other hand, focues mostly on _what_ we are doing, and ignores the _how_ we are doing it. This makes our code behave as an executable specification.

One extra benefit of declarative code is it's honesty: declarative code doesn't lie, it does what it says it does. This means we can take declarative code at face value and trust it.

This doesn't mean that declarative code doesn't need to prove that it does what it says it does during the process of writing tests, but instead that it adds an extra layer of confidence and rigor to our code.

Declarative code is not infalible, it can be corrupted. One way to corrupt declarative code is by bypassing the stablished rules in our model.

## A declarative Style of Design

A declarative style of design can only be achived when our model follows the techniques mentioned above: intention-revealing interfaces, side-effect-free functions and assertions.

A supple design not only enables a declarative style of design, but it can also lead to one. By adopting these techniques we can help migrate a non-declarative style of design in an old system int oa declarative one.

Supple design and a declarative style of design are not equivalent. A supple design just enable us to reduce the cost of friction that would require us to get to a declarative style of design. In other words, a supple design is a pre-requisit to achieve a declarative state of design.

## Drawing on Stablished Formalism

Starting a conceptual framework from scratch -specially on a new project- can be challenging. Most of the time, this is unnecesary and should be avoided.

Many domains -like math- already have a rich set of rules and laws already stablished. We don't need to re-invent the wheel, but instead we can draw our supple design on top of this prior-art.

This not only would save us a lot of time, but it would also provide us with all the richness and rigor that these field already have in place.
