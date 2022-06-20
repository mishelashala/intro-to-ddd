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

### Partnership Teams

Often in softare projects mutually dependent teams emerge. When this happens forge a partnertship within teams in order to ease development and to make sure both succeed.

This partnership will require the creation of processes to coordinate planing, development, management and integration between the teams. Both projects must accomodate the needs of the other in all the phases previously mentioned.

Teams in a partnership don't need to know all the internal details of each other.

### Shared Kernel

Continious integration, specially in projects with many and teams, can be slowed down by the inherent complexity of having to coordinate too many, or too big, teams. This is an expected side-effect that will generate race conditions between integrations, specially in uncoordinated environments.

These race conditions will end up causing a mismatch between already defined contracts and interfaces, causing conflicts and rework for the parts involved.

To combat this we must designate a small subset of the domain: a shared kernel. This subset must have the approval of all teams.

Aim to keep the shared kernel small. Only the minimum amount of functionality that supports the model should be accepted as part of it. If you need to extend the kernel, always build on top of it following the open-closed principle.

If something needs to be agreed on by all the teams before changing it, then that subset of functionally also must be migrated into the shared kernel. One good example of this is database tables and models.

The shared kernel will endup generating a upstream-downstream relationship with teams. To avoid slowing down other teams always use continious integration and versioning to avoid breaking existing functionally and to have breaking changes under control.

## Customer/Supplier Development

Upstream-downstream relationships between teams can be beneficiated by forging also a customer-supplier relatinship. This prevents downstream teams to be at complete mercy of the upstream team.

This customer-supplier relationship forces the upstream team to take into consideration the needs of the downstream team during the planning process.

### Comformist Team

When to teams decide to forge a client-supplier relationships but the upstream teams doesn't hold its commitment to take the downstream team's needs into account the relationship will end up deforming into a conformist relationships.

In this case upstream team will always cause delays on the work of downstream teams. Not only by not delivering what downstream teams need in time, but also in form. The upstream team can end up producing interfaces that don't match the needs of the downstream team, forcing the downstream team to rework.

When the relationships had deformed into a comformist one, the downstream team end up accepting its "fate". The only thing left for them is just to accept things as they are, and work with what they have[^sad].

### Anti Corruption Layer

When an organization adtops a shared kernel translations between contexts become defensive.

In a customer-supplier relationship the downstream team must protect its own model from upstream systems in order to maintain consistency. This is achieved thru the use of an isolation layer, also called an Anti-Corruption Layer (ACL from now on).

The need for isolation arises when upstream teams -or systems- have legacy systems. These legacy system can have weak modeling -or no modeling at all- compromosing as such the modeling of downstream systems.

The purpose of the ACL is to help isolating both system from the implementation details of each other. This is only possible by translating -and sometimes sanitizing- the models. The ACL can transform between models in one or both directions.

Upstream models show not have a direct impact in the internal models of downstream teams, but that doesn't mean its the responsibility of upstream teams to worry about how their modeling will impact others. There's always must be a contract agreement between parties, but if it's not possible to fulfill that contract "naturally" within the upstream modeling, then the ACL is a great way to "enforce" that contract externally.

### Open-Host services

Working with bounded contexts can lead to the need to have many translators for each integration a team has outside of their context. Having many instegrations can become demaning to the team -and the system-. The team can end up failling to fulfill all the needs of the translation layers.

To aliviate this problem we can pick a set of services that provide access to the system. These set of services will operate essentially as a protocol open for external integrations.

Once the protocol is stablished, only expand or extend your protocol when general -or common- needs arise. If a individual or specific need arises, then create a on-off translation for that specific need. By doing so, we can keep the protocol general purpose and maintain consistency.

By creating an open protocol for others to connect, intentionally or not, we transform the project into an upstream team in a customer-supplier relationship with other teams.

### Published Language

By using one-to-one translations between bounded contexts we can end up coupling teams and freezing development. Too many bounded contexts with too many translations is maintainability nightmare.

Instead, adopt a common published language that expresses all the domain information to aid teams. Let each team and subsystem translate directly from the published language instead of translating to each specific context. Translations can ocur, just like the ACL, in one or both directions.

The open-host protocol is a good example for the neeed of a published language in a project.

Always document the common medium of communication for the published language. The medium can be, http, sockets, buffers, etc.

### Separate Ways

When you encounter two sets of functionality that bare little or no significant relationship to each other, then let the teams go separate ways.

Split the teams by delcaring a new fully independent context.

### Big Ball of Mud

When systems grow without consisten modeling and/or consistent boundaries they eventually become Big Balls of Mud (BBoM from now on).

BBoM tend to keep growing and tend to become harder to work with over tiem. Logic inside BBoM become messy, contigent and confusing.

Due to the lack of structure onBBoM understanding them becomes hard. When a change needs to be made it is usually applied as patch, instead of a well thought piece functionallity, only exarcerbating the problem. This produces an endless cycle: the code is hard to understand, because of that we introduce a patch, the patch makes the code harder to understand.

It is extremely hard to "save" BBoM. The cost of labor is very intensive and the benefits -most of the time- are not worth the effort. It is better to quarantine BBoMs instead of refactoring them.

Always be aware of systems that can become BBoM. Adopt practices that help you avoiding the decay of systems: TDD, unit testing, refactoring.

### Distillation for Strategic Design

Distillation is the process of extracting the essence of what makes something useful. In software development modeling is a distillation process. Thru different means, like refactoring, we try to find the objects, the relationships and the rules that govern the domain. These elements for the essence and provide the bulk of the value in the domain.

By distilling the domain we achieve a deeper insight and understanding of the domain. Not only by identifying the elements of the domain, but also, by identifying what makes it useful.

From the distillation process, we can also find other subdomains (bounded contexts) and their corresponding models. This distillation process can lead us to have a strategic design, which, as discussed earlier, will help us coming up with a realistic plan for development.

### Generic Subdomains

While refactoring you can end up identifying cohesive subdomains, withe their corresponding models, that don't serve the main goal of the project. These subdomains can up serving only their own goals.

When this happens try to isolate this generic models into their own modules in order to create a separation of concers between the core and generic subdomains.

These generic subdomains probably will end up requiring further development and maintainence. If this need arises we must always prioritize the development of the core domain. We can assign a low priority to these modules and only work on them when the core domain doesn't demand our attention.

During the creation of these generic subdomains we must avoid spending too much time on them. We must avoid re-inventing the wheel as much as posible. We must try to use off-the-shelf pre-made solutions when possible.

To reiterate the point, all these strategies are in place to avoid diverting our attention and priorities from the core domain to the generic subdomains.

[^modular-monoliths]: See [Modular Monoliths](http://www.kamilgrzybek.com/design/modular-monolith-primer/)
[^micro-services]: See [Microservices](https://en.wikipedia.org/wiki/Microservices) on Wikipedia
[^inverse-conway-s-manouver]: See [Inverse Conway's Manouver](https://ctocraft.com/blog/how-can-the-inverse-conway-manoeuvre-help-drive-organisational-change/)
[^sad]: Sad, very sad
