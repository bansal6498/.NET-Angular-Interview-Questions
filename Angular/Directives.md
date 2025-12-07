## Directive
A Directive in Angular is a class that allows you to extend HTML’s capabilities. It allows you to attach behavior to elements in the DOM. 
### Types of Directives
-   **Component Directives:** The most common form, which has a template associated with it.
-  **Attribute Directives**: These change the appearance or behaviour of an element (e.g., `*ngIf`, `*ngFor`).
-   **Structural Directives**: These change the DOM layout by adding or removing elements  (e.g., `ngClass`, `ngStyle`).
#### What is the difference between an attribute directive and a structural directive in Angular?
**Answer:**
-   **Attribute Directives:** These modify the appearance or behaviour of an element, component, or other directive. They are applied as attributes on elements (e.g., ngClass, ngStyle).
-   **Structural Directives:** These change the structure of the DOM by adding or removing elements. They typically start with an asterisk (*) like *ngIf, *ngFor.
#### How do you create a custom directive in Angular?
**Answer:**
To create a custom directive in Angular:
1. Use Angular CLI to generate the directive:

        ng generate directive customDirectivee
2. In the directive class, use the `@Directive` decorator to specify the directive’s selector.
3. Implement the required logic using lifecycle hooks like `ngOnInit`, `ngOnChanges`, or `ngAfterViewInit`.
#### 🧩 Example
```ts
import { Directive, ElementRef, Renderer2 } from '@angular/core';
@Directive({
    selector: '[appHighlight]'
})
export class HighlightDirective {
    constructor(private el: ElementRef, private renderer: Renderer2) {
    this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', 'yellow');
    }
}
```
#### What is ngOnInit in directives, and when is it called?
**Answer:**
`ngOnInit` is a lifecycle hook in Angular that is called after the directive’s data-bound properties are initialized. This hook is typically used to perform initialization logic. It is called once after the directive’s constructor and before any other lifecycle hooks.
#### ngOnInit() vs constructor()
-   **constructor()** → Used for class initialization, dependency injection. Runs first.
-   **ngOnInit()** → Lifecycle hook, called once Angular initializes bindings. Best for data-fetching logic.
### Key Concepts of Directives in Angular
1. **Selectors:** Directives are applied to DOM elements via a selector. The selector can be:
    -   **Element Selector:** Applied as an HTML element tag.
        #### 🧩 Example
        ```ts
        @Directive({ selector: 'appCustomDirective' })
        ```
    -   **Attribute Selector:** Applied to an element via its attribute.
        #### 🧩 Example
        ```ts
        @Directive({ selector: '[appCustomDirective]' })
        ```
    -   **Class Selector:** Applied when the element has a specific class.   
        #### 🧩 Example
        ```ts
        @Directive({ selector: '.appCustomDirective' })
        ```
2.  **Host Binding:** Directives can manipulate properties of the element they are attached to using `@HostListener`.
    #### 🧩 Example
    ```ts
    @HostListener('click') onClick() {
        console.log('Element clicked!');
    }
    ```
#### How do you apply a structural directive in Angular?
**Answer:**
A structural directive is applied to an element by prefixing it with an asterisk (*). It alters the structure of the DOM, such as adding or removing elements. For example, `*ngIf` is a structural directive used to conditionally display an element.
```html
<div *ngIf="isVisible">This text is conditionally rendered based on isVisible.</div>
```
#### What is the purpose of ng-template in structural directives?
**Answer:**
`ng-template` is used in Angular to define a block of HTML that can be conditionally rendered or used by structural directives such as `*ngIf` or `*ngFor`. It is a way to define content that is not rendered immediately but can be inserted into the DOM when required.
```html
<ng-template [ngIf]="isVisible">
<div>This content is conditionally displayed based on isVisible.</div>
</ng-template>
```
#### How do you pass data to a directive?
**Answer:**
You can pass data to a directive using input properties. The directive’s input properties are defined using the `@Input()` decorator, and they allow you to pass values from the parent component.
```ts
@Directive({
    selector: '[appHighlight]'
})
export class HighlightDirective {
    @Input() appHighlight: string;
    constructor(private el: ElementRef, private renderer: Renderer2) {}
    ngOnInit() {
        this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', this.appHighlight);
    }
}
```
In the component HTML:
```html
<div [appHighlight]="'yellow'">This text is highlighted.</div>
```
#### What is @HostBinding in Angular directives?
**Answer:**
`@HostBinding` is a decorator that binds a property of the directive to a property of the host element. It allows you to set properties or attributes of the host element from within the directive.
```ts
@HostBinding('style.backgroundColor') backgroundColor: string;
constructor() {
    this.backgroundColor = 'yellow';
}
```
This will set the background colour of the host element to yellow when the directive is applied.
#### Can you use multiple directives on the same element?
**Answer:**
Yes, you can apply multiple directives to the same element in Angular. However, some directives (especially structural ones) may conflict with each other if they manipulate the DOM structure. Non-structural directives (like attribute directives) can be applied together without conflict.
```html
<div appHighlight appBorder>Content with multiple directives</div>
```
In this example, both appHighlight and appBorder can be applied to the same element without conflict.
#### What is a viewContainerRef in Angular and how is it used in directives?
**Answer:**
`ViewContainerRef` is an Angular service that represents a container where views can be attached. It is typically used in structural directives for dynamically adding or removing views.
```ts
import { Directive, ViewContainerRef, TemplateRef } from '@angular/core';
@Directive({
    selector: '[appIf]'
})
export class IfDirective {
    constructor(private viewContainer: ViewContainerRef, private templateRef: TemplateRef<any>)
    {}
    @Input() set appIf(condition: boolean) {
        if (condition) {
            this.viewContainer.createEmbeddedView(this.templateRef);
        } else {
        this.viewContainer.clear();
        }
    }
}
```
This directive uses `ViewContainerRef` to dynamically insert or remove the element depending on the condition.
#### What is the lifecycle of a directive in Angular?
**Answer:**
The lifecycle of a directive is similar to that of a component. The main lifecycle hooks for a directive are:
-   **ngOnChanges:** Called when the directive’s input properties change.
-   **ngOnInit**: Called once the directive is initialized.
-   **ngDoCheck**: Called to check for changes in the directive.
-   **ngAfterViewInit**: Called after the directive's view has been initialized.
-   **ngOnDestroy**: Called when the directive is destroyed.</br>
These lifecycle hooks help manage the behaviour of the directive and react to changes in input properties, view initialization, and cleanup.