## PIPE
In Angular, a pipe is a way to transform data in templates. It is a mechanism for applying transformations to data before displaying it in the view, such as formatting dates, filtering lists, or changing the case of text. Pipes can be applied directly in the template and are particularly useful for modifying the format or appearance of data without modifying the underlying data model. Pipes are similar to filters in AngularJS but are more efficient and flexible in Angular (2+).
### Types of Pipes:
-   **Pure Pipes:** By default, pipes are pure, meaning they only re-execute when the input data changes. Angular caches the result for better performance.
-   **Impure Pipes:** Impure pipes re-execute on every change detection cycle, even if the input data has not changed.
-   **Built-in Pipes:** Angular comes with several built-in pipes, such as DatePipe, CurrencyPipe, UpperCasePipe, etc.
-   **Custom Pipes:** You can create your own custom pipes to implement specific transformation logic for data in your application.
#### Basic Syntax of Using a Pipe:
In an Angular template, pipes are applied with the | symbol.
```ts
{{ value | pipeName }}
```
### Create the custom PIPE
1.  
        ng generate pipe pipes/custom
this will create two files-

        custom.pipe.ts
        custom.pipe.spec.ts

2.  Write Custom Pipe Code

#### Example- Transforms hello world → Hello world
```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'capitalize'
})
export class CapitalizePipe implements PipeTransform {

  transform(value: string): string {
    if (!value) return value;
    return value.charAt(0).toUpperCase() + value.slice(1);
  }

}

```
3.  Use Pipe in Component Template
```html
<p>{{ 'angular pipe' | capitalize }}</p>
```
#### What is the purpose of pipes in Angular?
**Answer:**
Pipes in Angular are used to transform data in templates before displaying it in the view. They allow you to format data, change its appearance, or apply custom transformations without altering the underlying data model. Common use cases include formatting dates, currency, and text, as well as filtering or sorting lists.
#### How do you create a custom pipe in Angular?
**Answer:**
To create a custom pipe in Angular, you need to implement the `PipeTransform` interface and define the transform method that accepts input data and returns the transformed output. The custom pipe should be decorated with the `@Pipe` decorator and registered in the module.
#### How do you apply a pipe in an Angular template?
**Answer:**
In Angular templates, pipes are applied using the | symbol followed by the pipe name. If you need to pass parameters to the pipe, you can specify them after the colon (:). For example:
```html
<p>{{ amount | currency: 'USD' }}</p>
```
#### Can pipes accept parameters in Angular?
**Answer:**
Yes, pipes can accept parameters. Parameters are passed after the pipe name, separated by colons. For example:
```html
<p>{{ value | date: 'shortDate' }}</p>
```
You can also pass multiple parameters. For instance:
```html
<p>{{ amount | currency: 'USD': true }}</p>
```
Here, the second parameter true indicates that the currency symbol should be included.
#### What are some built-in pipes available in Angular?
**Answer:**
Some of the commonly used built-in pipes in Angular include:
-   **DatePipe**: For formatting dates.
-   **CurrencyPipe**: For formatting numbers as currency.
-   **UpperCasePipe**: For converting text to uppercase.
-   **LowerCasePipe**: For converting text to lowercase.
-   **JsonPipe**: For converting objects to JSON format for display.
-   **SlicePipe**: For slicing an array or string.
#### How can you optimize performance when using pipes in Angular?
**Answer:**
To optimize performance:
-   Use `pure pipes` for simple data transformations that do not need frequent recalculation.
Pure pipes are more efficient because they only re-execute when their inputs change.
-   Avoid using `impure pipes` unless absolutely necessary, as they can be called on every change detection cycle.
-   Use `trackBy` in ngFor with large lists to improve the performance of the rendering and avoid unnecessary recalculations.
#### Can pipes be used with observables in Angular?
**Answer:**
Yes, pipes can be used with observables in Angular. The async pipe is commonly used to subscribe to observables in templates and automatically unsubscribe when the component is destroyed.</br>
-    Subscribes to an Observable/Promise and returns latest value.
-    Handles subscription + unsubscription automatically.
```html
<p>{{ observableData | async }}</p>
```
#### What is the difference between a pure and impure pipe in Angular?
**Answer:**
-   **Pure Pipe:** A pipe is pure by default. It only re-executes when the input data changes, making it more efficient because Angular caches the result.
-   **Impure Pipe:** An impure pipe runs on every change detection cycle, regardless of whether the input data changes. It is typically used when the input data might change frequently and needs to be recalculated often, like arrays or objects that are mutated.