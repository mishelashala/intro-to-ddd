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
