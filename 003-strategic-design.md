# Strategic Design

Software development requires strategies for design and development: how are we gonna design and develop our system?

The most common approach is to divide our application into smaller pieces in order to make it more managable. But then the question arises: what cretieria are gonna use for that?

DDD promotes the idea of dividing our system into smaller pieces following a bounded-context approach.

A bounded-context acts as a boundary description. This description doesn't tell us anything about its form, but about its responsibilities. This means that a bounded context can be a susbystem or the work of an entire development team.

Bounded contexts can be part of an entire system taking the form of modules, services or sub-applications[^modular-monoliths]; or completely independent systems[^micro-services].

By following this strategy design process we influence not only the code, but the way we write the code. This leads to structure processes, operations, policies, teams and interactions around bounded contexts[^inverse-conway-s-manouver].

## Teams Topologies

As mentioned above, by describing and delimiting the bounded contexts in a project we can achieve an inverse conway manouver. Avobe there are some team topologies listed that emerge when we follow this approach.

### Upstream-Downstream Relationship Between Teams

The upstream-downstream relationships between teams is an analogy of the flow of the water of the river. A person located downstream the river is at the mercy of whatever the person upstream the river throws at the water.

This relationship arises when there's a dependency between two (2) teams. The downstream team depends on the work of the upstream team in order to succeed.

One common example of this relationship is a team that is developing a UI library that is gonna be used by other team. The team that is developing the UI library is the upstream team in this example, and the team using that UI library is the downstream team.

The upstream team not only, in some circunstances, slow down significatively the work of the downstream team, but it can also make the downstream team fail at delivery.

### Mutually Dependent Teams

Sometimes in an organization two (2) teams can be completely independent and work in two separate bounded contexts, but in order for both to succeed they must deliver their work at the same time.

This is a strange all or nothing situation, if one team doesn't deliver, even when they are completely independent, both teams fail at delivery.

### Free Team

A free team is one such that its software project has little or no effect on other projects when its delivered.

In projects with bounded contexts where strong boundaries exist and there's no need for translation and communication with other bounded contexts free teams can, and will, emerge.

As long as free teams deliver, they must be left alone to operate in an autonomous manner.

### Context Map

During the phase development and design we must identify models. And, when possible, define them as bounded contexts.

Bounded context, as many other elements we have previously discussed, must be part of the ubiqutious language.

It is no strange for bounded contexts to require communication between them. We must identify and describe these points of contact and their corresponding translation mechanisms.

We can employ a map to show all the bounded contexts with all their corresponding boundaries. Once this stablished we can draw the contact points between them, and finally we can start thinking -and drawing- the translation mechanisms in the map.

Since we are mapping out all the boundaries and contexts in our system we can use this map as a realistic plan during the strategic design phase.

In order for development to have a strategic plan, first we must have a realistic plan and a deep understanding of the problem. The map not only helps us documenting the contexts and relationships, but it also forces us to think in teams of a realistic design.

[^modular-monoliths]: See [Modular Monoliths](http://www.kamilgrzybek.com/design/modular-monolith-primer/)
[^micro-services]: See [Microservices](https://en.wikipedia.org/wiki/Microservices) on Wikipedia
[^inverse-conway-s-manouver]: See [Inverse Conway's Manouver](https://ctocraft.com/blog/how-can-the-inverse-conway-manoeuvre-help-drive-organisational-change/)
