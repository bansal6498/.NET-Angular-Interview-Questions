## Data Binding
### Explain Object Call Bind in Angular
In Angular, Object Binding typically refers to **two-way binding** or **one-way binding**.
-   **One-way binding**: Data flows in one direction, either from the component to the view (`{{expression}}` in the template) or from the view to the component (`[(ngModel)]` for forms).
#### 🧩 Example
```html
<div>{{ name }}</div> <!-- One-way data binding -->
```
-   **Two-way binding:** This allows data to flow in both directions: from the component to the view, and from the view to the component. This is achieved using the ngModel directive.
#### 🧩 Example
```html
<input [(ngModel)]="name" /> <!-- Two-way data binding -->
```
### Binding in Angular:
-   **Interpolation** Interpolation allows you to embed expressions inside the HTML to display dynamic values.
#### 🧩 Example
```html
<p>{{ message }}</p>
```
-   **Property Binding:** Binds properties of HTML elements to component properties.
#### 🧩 Example
```html
<img [src]="imageUrl" />
```
-   **Event Binding:** Binds an event to a method.
#### 🧩 Example
```html
<button (click)="handleClick()">Click Me</button>
```
-   **Two-way Binding:** Combines property and event binding for form elements like inputs.
#### 🧩 Example
```html
<input [(ngModel)]="name" />
```
#### What is the difference between interpolation and property binding in Angular?
**Answer:**
Interpolation is used for displaying dynamic data in the view using `{{ expression }}`, whereas property binding is used to bind a property of an HTML element to a component property using `[property]="expression"`.
### Passing Data from Parent to Child Or Vice Versa
In Angular, there are different mechanisms for passing data between a parent and a child component. Here's how you can achieve both scenarios:</br>
#### **Passing Data from Parent to Child:**
To pass data from a parent component to a child component, we can use `@Input()` decorator in the child component to receive the data.
-   **Parent Component:** Pass data to the child component using property binding.
-   **Child Component:** Receive data using the `@Input()` decorator.
#### 🧩 Example
Parent Component (app.component.ts):
```ts
import { Component } from '@angular/core'
@Component({
    selector: 'app-root',
    template: `<app-child [parentData]="dataFromParent"></app-child>`
})
export class AppComponent {
    dataFromParent = 'Hello from Parent';
}
```
Child Component (child.component.ts):
```ts
import { Component, Input } from '@angular/core';
@Component({
selector: 'app-child',
template: `<p>{{ parentData }}</p>`
})
export class ChildComponent {
    @Input() parentData: string; // Receives data from parent
}
```
Here, parentData is passed from the parent component to the child using `[parentData]="dataFromParent"`.
#### **Passing Data from Child to Parent:**
To pass data from a child to a parent, we use `@Output()` along with EventEmitter. The child component will emit an event, and the parent component will listen to that event.
-   **Child Component:** Emit data to the parent component using the `@Output()` decorator and `EventEmitter`.
-   **Parent Component:** Listen for the emitted event using event binding.
#### 🧩 Example
Parent Component (app.component.ts):
```ts
import { Component } from '@angular/core';
@Component({
    selector: 'app-root',
    template: `<app-child (childEvent)="receiveData($event)"></app-child>`
})
export class AppComponent {
    receiveData(data: string) {
        console.log('Data from Child:', data);
    }
}
```
Child Component (child.component.ts):
```ts
import { Component, Output, EventEmitter } from '@angular/core';
@Component({
    selector: 'app-child',
    template: `<button (click)="sendData()">Send Data to Parent</button>`
})
export class ChildComponent {
    @Output() childEvent = new EventEmitter<string>();
    sendData() {
        this.childEvent.emit('Hello from Child'); // Emit data to parent
    }
}
```
In this example, the `childEvent` is emitted from the child component, and the parent component listens to this event using `(childEvent)="receiveData($event)"`.</br>
-   **@Input()** → Pass data from parent → child.
-   **@Output()** → Emit events from child → parent.
-   **@ViewChild()** → Access child component/template element directly in parent.