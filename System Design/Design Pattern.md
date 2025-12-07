## Design Pattern
-   **Singleton Pattern**: Ensures that a class has only one instance and provides a global point of access.
-   **Factory Pattern**: Defines an interface for creating an object, but allows subclasses to alter the type of created objects.
-   **Observer Pattern**: Used to allow a subject to notify its observers of changes, typically used in event-driven programming.
-   **Decorator Pattern**: Allows functionality to be added to an object dynamically.
-   **Strategy Pattern**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.
-   **Repository Pattern**: Used for accessing data from different sources in a clean and decoupled way.
#### Which design patterns have you worked with? (short list + when to use)
**Answer:**
Common strong interview answer (give real examples from your work):

-   **Repository + Unit of Work** — abstract DB access, testable data layer.
-   **Factory / Abstract Factory** — create objects where concrete type decided at runtime.
-   **Singleton** — single shared resource (cache, configuration) — be careful with state.
-   **Strategy** — swap algorithms (e.g., validation, pricing rules).
-   **Decorator** — extend behavior (e.g., adding logging, caching).
-   **Adapter / Facade** — integrate legacy systems or simplify subsystems.
-   **Observer / Pub-Sub** — events, notifications, domain events.
-   **Mediator (e.g., MediatR)** — decouple request/handling flow (useful in CQRS).
-   **Command** — encapsulate actions for undo/redo or queued processing.
-   **CQRS & Event Sourcing** — for systems needing scalability and auditability.
-   **Dependency Injection** — built-in DI in .NET Core (infrastructure / lifetime management).
