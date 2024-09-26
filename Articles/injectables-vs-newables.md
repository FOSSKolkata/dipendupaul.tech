## **Injectables Vs Newables**

Injectables are Services like factories, repositories,  application services, infrastructure services. etc., Newables are entities and value objects. 

Two fundamental constraints apply to the concepts of newables and injectables:

1. Newables **must not** depend on injectables and
2. Injectables **must not** hold newables as their state (object attributes).

As the name suggests, injectables should never be newed up but should always be injected. Exception to this guideline is the Main method and IOC containers which can assume the responsibility of newing up or instantiating Injectables. 

Similarly, a newable should not be injected, but it can be newed up by a service, like a factory, or another newable.

A newable should not depend upon an injectable. This often results in a violation of single responsibility, for example, a mail entity taking the extra responsibility of sending itself, or an invoice entity taking the extra responsibility of persisting itself into the database. Ofcourse, to assume these responsibilities, these entities would have depended upon some services, and due to these dependencies, testing these newables would become complicated.

Injectables should depend upon other injectables, but should never depend upon newables. If an injectable violates this rule and contains a newable in its state, it can result in side effects that are difficult to debug and complicate testing.


### Resources

https://www.giorgiosironi.com/2009/07/when-to-inject-distinction-between.html