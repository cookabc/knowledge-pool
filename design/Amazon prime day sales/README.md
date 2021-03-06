## [Amazon Prime Day Sales](https://twitter.com/alexxubyte/status/1546520282571034625)

> Amazon Prime days are coming. Designing a system with extremely high concurrency, high availability, and quick responsiveness needs to consider many aspects ๐๐ฅ๐ฅ ๐ญ๐ก๐ ๐ฐ๐๐ฒ ๐๐ซ๐จ๐ฆ ๐๐ซ๐จ๐ง๐ญ๐๐ง๐ ๐ญ๐จ ๐๐๐๐ค๐๐ง๐.

๐๐ก๐๐ง ๐ข๐ฌ ๐ญ๐ก๐ ๐ฌ๐ฒ๐ฌ๐ญ๐๐ฆ ๐ฎ๐ฌ๐๐๐ฎ๐ฅ?
- When a rare or very popular product is released: new iPhones, PS5, etc.
- Limited-time sales: Black Friday sales, Amazon Primday day, etc.

![amazon_sale](amazon_sale.jpeg)

๐๐๐ฌ๐ข๐ ๐ง ๐ฉ๐ซ๐ข๐ง๐๐ข๐ฉ๐ฅ๐๐ฌ:

1. Less is more. Fewer elements on the web page, fewer data queries to the database, fewer web requests, fewer system dependencies

2. Short critical path. Fewer hops among services or merge into one service

3. Async. Use message queues to handle high TPS

4. Isolation. Isolate static and dynamic contents, isolate processes and databases for rare items

5. Overselling is bad. When and how to manage the inventory is important

6. User experience is important. We donโt want to inform users that they have successfully placed orders but later tell them no items are actually available