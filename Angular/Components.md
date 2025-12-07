## Components
Components are the building blocks of an Angular application. Each component has:
-   A template (HTML)
-   A class (logic and data binding)
-   A stylesheet (CSS)
#### 🧩 Example
```typescript
// app.component.ts
import { Component } from '@angular/core';
@Component({
    selector: 'app-root',
    template: '<h1>Welcome to {{ title }}</h1>',
    styleUrls: ['./app.component.css']
})
export class AppComponent {
    title = 'Angular App';
}
```
#### What are Components and Modules in Angular?
**Answer:**
-   Components  
    -   The building blocks of an Angular application.
    -   Each component controls a view (UI part).
    -   A component has:
        -   TypeScript file (logic)
        -   HTML template (UI)
        -   CSS/SCSS (styles)
        -   Metadata (via @Component decorator).
    ```ts
    @Component({
        selector: 'app-user',
        templateUrl: './user.component.html',
        styleUrls: ['./user.component.css']
    })
    export class UserComponent {
        name = 'Priyanshu';
    }
    ```
-   Modules
    -   A way to organize and group related components, directives, pipes, and services.
    -   Defined using `@NgModule`.
    -   The root module is usually `AppModule`.
    -   Helps with lazy loading and code organization.  
    ```ts
    @NgModule({
        declarations: [UserComponent],
        imports: [BrowserModule, FormsModule],
        bootstrap: [AppComponent]
    })
    export class AppModule {}
    ```