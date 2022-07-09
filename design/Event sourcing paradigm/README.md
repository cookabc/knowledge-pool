## [How do we design a system using the 𝐞𝐯𝐞𝐧𝐭 𝐬𝐨𝐮𝐫𝐜𝐢𝐧𝐠 paradigm?](https://twitter.com/alexxubyte/status/1539999422485913600)

> How do we design a system using the 𝐞𝐯𝐞𝐧𝐭 𝐬𝐨𝐮𝐫𝐜𝐢𝐧𝐠 paradigm? How is it different from normal system design? What are the benefits? We will talk about it in this post.
> 
> The diagram below shows the comparison of a normal CRUD system design with an event sourcing system design. We use an e-commerce system that can place orders and pay for the orders to demonstrate how event sourcing works.

> The event sourcing paradigm is used to design a system with determinism. This changes the philosophy of normal system designs.
>
> How does this work? Instead of recording the order states in the database, the event sourcing design persists the events that lead to the state changes in the event store. The event store is an append-only log.
> 
> The events must be sequenced with incremental numbers to guarantee their ordering. The order states are rebuilt from the events and maintained in OrderView. If the OrderView is down, we can always rely on the event store which is the source of truth to recover the order states.
> 
> Let's look at the steps in detail.

![event_sourcing](event_sourcing.jpeg)

🔹Non-Event Sourcing

- Steps 1 and 2: Bob wants to buy a product. The order is created and inserted into the database.
- Steps 3 and 4: Bob wants to change the quantity from 5 to 6. The order is modified with a new state.
- Steps 5 and 6: Bob pays $60 for the order. The order is complete and the state is Paid.
- Steps 7 and 8: Bob queries the latest order state. Query service retrieves the state from the database.

🔹Event Sourcing

- Steps 1 and 2: Bob wants to buy a product. A NewOrderEvent is created, sequenced and stored in the event store with eventID=2001.
- Steps 3 and 4: Bob wants to change the quantity from 5 to 6. A ModifyOrderEvent is created, sequenced, and persisted in the event store with eventID=2002.
- Steps 5 and 6: Bob pays $60 for the order. An OrderPaymentEvent is created, sequenced, and stored in the event store with eventID=2003. Notice the different event types have different event attributes.
- Step 7: OrderView listens on the events published from the event store, and builds the latest state for the orders. Although OrderView receives 3 events, it applies the events one by one and keeps the latest state.
- Step 8: Bob queries the order state from OrderService, which then queries OrderView. OrderView can be in memory or cache and does not need to be persisted, because it can be recovered from the event store.