### ng run vs ng build vs ng serve
| 🔹 **Feature** | **ng run** | **ng build** | **ng serve** |
|----------------|----------------|----------------| ---------------|
| Purpose | Runs a specific architect target for a project, as defined in the angular.json file. | Compiles the application into static files that can be deployed to a web server. | Builds the app in memory and serve it using a local development server (with hot reloading) |
| When to Use | Used for custom configurations or executing a specific task, such as deploying an application or building it with specific options. | Used to prepare app for production by creating the `dist` folder with optimized, minified files. | Used for local development to view changes immediately in browser without needing to manually rebuild or restart the server. |
#### Conclusion
1. Use ng build:
    -   When preparing the app for deployment.
    -   To create optimized, production-ready static files.
2. Use ng serve:
    -   For local development and debugging.
    -   To take advantage of hot-reloading for faster iteration.
3. Use ng run:
    -   For running custom tasks, such as deploying the app or testing with specific configurations.
#### What are signals in Angular, and advantages over earlier approaches?
**Answer:**
-   **Signals** are a reactive primitive introduced in modern Angular versions — a low-level observable-like value that tracks dependencies and triggers updates when changed.
-   **Advantages:**
    -   Fine-grained reactivity: only components or computed values that depend on a signal update — smaller change detection footprint.
    -   Simpler mental model for state (no need to use `ChangeDetectorRef` or rely on zone trickery).
    -   Works well with the new reactivity-based rendering model and improves performance compared to full-zone-based change detection or relying solely on RxJS for component state.</br>
(If asked, mention `signal`, `computed`, and `effect` APIs and show a small example.)
#### Difference: Subject, BehaviorSubject, ReplaySubject (RxJS), NgRx
**Answer:**
-   **Subject**: multicast observable — no initial value, subscribers only get future values.
-   **BehaviorSubject**: holds the latest value and emits it immediately to new subscribers; requires an initial value.
-   **ReplaySubject**: replays a specified number of past values (or all) to new subscribers.
-   **NgRx**: Full **Redux-style** state management with Actions, Reducers, Effects. Best for large-scale, complex state.</br>

Use cases:
    -   Use `BehaviorSubject` for current state (e.g., auth state).
    -   Use `ReplaySubject` for replaying events or caching last N values.
    -   Use `Subject` for event/stream where no prior state is needed.
#### What is an HTTP Interceptor in Angular?
**Answer:**
An HTTP Interceptor is a service that implements `HttpInterceptor` and can intercept & modify outgoing HTTP requests and incoming responses. Common uses:
-   Add auth headers (JWT).
-   Handle token refresh on 401.
-   Global error handling.
-   Request/response logging.
-   Set timeouts or retry logic.
#### 🧩 Example
```ts
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler) {
    const token = this.authService.getToken();
    const cloned = token ? req.clone({ setHeaders: { Authorization: `Bearer ${token}` }}) : req;
    return next.handle(cloned);
  }
}
```
#### How do you implement resilience in Angular?
**Answer:**
AnsweResilience is about handling network failures, slow responses, and transient issues.</br> 
Practical patterns:
-   **Retry with backoff**: use retryWhen + exponential backoff.
-   **Timeouts**: use timeout() operator or AbortController.
-   **Circuit breaker**: client-side circuit-breaker libraries (or simple counters) to stop hitting failing endpoints.
-   **Caching / stale-while-revalidate**: store responses (in-memory or IndexedDB) to serve while fetching fresh data.
-   **Request deduplication**: collapse identical concurrent requests so only one HTTP call goes out.
-   **Graceful error handling & fallback UI**: show offline/skeleton states and informative messages.
-   **Global error interceptor**: handle auth expiry (refresh token), unify error handling and logging.
-   **Offline support**: Service Workers, local cache, optimistic UI updates where appropriate.
-   **Monitoring & telemetry**: capture client-side errors & performance (Sentry, App Insights).
#### 🧩 Example
```ts
http.get('/api/data').pipe(
  retryWhen(errors => errors.pipe(
    scan((i, err) => i + 1, 0),
    delayWhen(retryCount => timer(Math.pow(2, retryCount) * 1000)),
    takeWhile(retryCount => retryCount < 4)
  ))
)
```
#### ChangeDetectionStrategy.OnPush
**Answer:**
-   Default strategy → Angular checks the entire component tree.
-   **OnPush** → Angular checks only when:
    -   Input reference changes
    -   An event is triggered inside component
    -   Observable emits data
-   ✅ Optimizes performance by reducing unnecessary checks.
#### Dependency Injection (DI) in Angular
**Answer:**
-   Angular has a hierarchical injector system.
-   Services can be provided at root level (`providedIn: 'root'`) or component level.
-   Ensures singleton services and promotes testability.
#### What are “signals” in Angular, and what is their advantage over earlier approaches?
**Answer:**
-   **Signals** (introduced in Angular 16) are a new reactivity model for managing state.
-   A **signal** is basically a reactive variable that holds a value and notifies the framework when it changes.
#### Example
```ts
import { signal } from '@angular/core';

count = signal(0);

increment() {
  this.count.set(this.count() + 1);
}
```
-   Here, `count` is a signal. Accessing it via `this.count()` gives its value, and `ß` updates it.
#### Advantages over earlier approaches (like @Input(), RxJS subjects, or ChangeDetectionStrategy.OnPush):
1.  **Fine-grained reactivity** → Only the components depending on the signal are updated, instead of running Angular’s full change detection cycle.
2.  **Simpler than RxJS for local state** → No need to manage subscriptions manually.
3.  **Better performance** → Signals integrate with Angular’s change detection, avoiding unnecessary re-renders.
4.  **Predictable data flow** → Unlike zone.js-based detection, signals are explicit and easier to debug.
5.  **Future-ready** → Angular team is moving toward a Zoneless Angular where Signals will be the backbone of reactivity.</br>
#### 👉 You can summarize:
“Signals are Angular’s new reactivity model that provide fine-grained, efficient updates without requiring zone.js. They make state management simpler, more predictable, and improve performance over traditional RxJS and change detection approaches.”