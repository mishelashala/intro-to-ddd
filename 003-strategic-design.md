# Strategic Design

Software development requires strategies for design and development: how are we gonna design and develop our system?

The most common approach is to divide our application into smaller pieces in order to make it more managable. But then the question arises: what cretieria are gonna use for that?

DDD promotes the idea of dividing our system into smaller pieces following a bounded-context approach.

A bounded-context acts as a boundary description. This description doesn't tell us anything about its form, but about its responsibilities. This means that a bounded context can be a susbystem or the work of an entire development team.

Bounded contexts can be part of an entire system taking the form of modules, services or sub-applications[^modular-monoliths]; or completely independent systems[^micro-services].

By following this strategy design process we influence not only the code, but the way we write the code. This leads to structure processes, operations, policies, teams and interactions around bounded contexts[^inverse-conway-s-manouver].

## Teams Topologies

As mentioned above, by describing and delimiting the bounded contexts in a project we can achieve an inverse conway manouver. Avobe there are some team topologies listed that emerge when we follow this approach.

[^modular-monoliths]: See [Modular Monoliths](http://www.kamilgrzybek.com/design/modular-monolith-primer/)
[^micro-services]: See [Microservices](https://en.wikipedia.org/wiki/Microservices) on Wikipedia
[^inverse-conway-s-manouver]: See [Inverse Conway's Manouver](https://ctocraft.com/blog/how-can-the-inverse-conway-manoeuvre-help-drive-organisational-change/)
