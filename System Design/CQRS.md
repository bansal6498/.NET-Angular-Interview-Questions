## CQRS- Command Query Responsibility Segregation
#### What is CQRS? How have you implemented it?
**Answer:**
**CQRS** = Command Query Responsibility Segregation: separate the model for **writes (commands)** from the model for **read(queries)**.
Typical implementation:
-   **Write side**: Accept commands, apply business logic, update write DB, publish events.
-   **Read side**: Optimized read models/denormalized views (can be separate DB) to serve queries fast.
-   **Eventing**: Optionally use events to synchronize read models (eventually consistent).
-   **Tools**: MediatR for dispatching commands/queries, Kafka/RabbitMQ/Azure Service Bus for events, separate read-DB (e.g., read replicas, ElasticSearch, Redis).
-   **Use cases**: complex domains with heavy read vs write patterns, scalability needs, or when you need different schemas for reads/writes.</br>

Use MediatR for in-process command/query dispatch, handled commands in transactional boundaries (EF transaction), published domain events to RabbitMQ, and updated denormalized read models consumed by the frontend. Reads were served from a separate read-optimized store (SQL/Elastic).”