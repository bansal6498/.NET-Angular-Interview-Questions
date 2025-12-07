## Forms
Forms are fundamental building blocks for collecting and managing user input in Angular applications. Angular provides two main approaches for handling forms: 
### Reactive Forms (Model-Driven Approach):
-   Forms are defined programmatically in the component class.
-   Provides better control over form validation and dynamic form creation.
-   Works well for complex forms with a lot of interactivity.
### Template-Driven Forms (Template-Driven Approach):
-   Forms are defined in the HTML template using directives.
-   Suitable for simpler forms.
-   Validation is declared in the template using Angular directives.

| 🔹 **Feature** | **Reactive Forms** | **Template-Driven Forms** |
|----------------|----------------|----------------|
| Approach | Programmatic (Model-Driven). | Declarative (Template-Driven). |
| Setup | Form structure and validations are defined in the component class. | Form structure and validations are defined in the template. |
| Validation | Validation logic is handled in the component class. | Validation logic is defined using directives in the template. |
| Scalability | Better for large and complex forms.| Suitable for simpler forms. |
| Testing | Easier to unit test because it’s more programmatic. | Harder to test due to dependency on templates. |
| Performance | Better for performance as it doesn't rely heavily on templates. | Less efficient due to the dependency on Angular's template parser. |
### Reactive Forms
Reactive forms provide a more programmatic and flexible way to handle forms.
#### Key Concepts
1. **FormControl:** Tracks the value and validation status of an individual form input.
2. **FormGroup:** Tracks the value and validation status of a group of inputs.
3. **FormBuilder:** A service to simplify the creation of FormGroup and FormControl.
#### 🧩 Example

Component File (app.component.ts)

```ts
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
})
export class AppComponent {
    registrationForm: FormGroup;
    constructor(private fb: FormBuilder) {
    this.registrationForm = this.fb.group({
        username: ['', [Validators.required, Validators.minLength(3)]],
        email: ['', [Validators.required, Validators.email]],
        password: ['', [Validators.required, Validators.minLength(6)]],
    });
    }
    onSubmit() {
        console.log(this.registrationForm.value);
    }
}
```
Template File (app.component.html)
```html
// <form [formGroup]="registrationForm" (ngSubmit)="onSubmit()">
<label for="username">Username:</label>
<input id="username" formControlName="username">
<div *ngIf="registrationForm.get('username')?.invalid &&
registrationForm.get('username')?.touched">
Username is required and must be at least 3 characters.
</div>
<label for="email">Email:</label>
<input id="email" formControlName="email">
<div *ngIf="registrationForm.get('email')?.invalid && registrationForm.get('email')?.touched">
Enter a valid email address.
</div>
<label for="password">Password:</label>
<input id="password" type="password" formControlName="password">
<div *ngIf="registrationForm.get('password')?.invalid &&
registrationForm.get('password')?.touched">
Password must be at least 6 characters.
</div>
<button type="submit" [disabled]="registrationForm.invalid">Submit</button>
</form>
```
### Template Driven Forms
Template-Driven Forms rely on Angular's two-way data binding and directives to handle user input.
#### Key Concepts
1. Uses Angular directives like ngModel, ngForm, and required.
2. Validation is declared directly in the template using directives like required, minlength, etc.
#### 🧩 Example

Component file (app.component.ts)

```ts
import { Component } from '@angular/core';
@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
})
export class AppComponent {
    onSubmit(form: any) {
        console.log(form.value);
    }
}
```
Template File (app.component.html)
```html
<form #registrationForm="ngForm" (ngSubmit)="onSubmit(registrationForm)">
<label for="username">Username:</label>
<input id="username" name="username" ngModel required minlength="3">
<div *ngIf="registrationForm.controls['username']?.invalid &&
registrationForm.controls['username']?.touched">
Username is required and must be at least 3 characters.
</div>
<label for="email">Email:</label>
<input id="email" name="email" ngModel required email>
<div *ngIf="registrationForm.controls['email']?.invalid &&
registrationForm.controls['email']?.touched">
Enter a valid email address.
</div>
<label for="password">Password:</label>
<input id="password" type="password" name="password" ngModel required minlength="6">
<div *ngIf="registrationForm.controls['password']?.invalid &&
registrationForm.controls['password']?.touched">
Password must be at least 6 characters.
</div>
<button type="submit" [disabled]="registrationForm.invalid">Submit</button>
</form>
```
### When to Use Reactive Forms vs. Template-Driven Forms
#### Use Reactive Forms when:
-   The form is complex with nested groups.
-   You need to dynamically add or remove form controls.
-   Unit testing and reusability are critical.
#### Use Template-Driven Forms when:
-   The form is simple and doesn’t require much customization.
-   You prefer a declarative approach with minimal code in the component.

| Feature     | Template-driven                          | Reactive                              |
| ----------- | ---------------------------------------- | ------------------------------------- |
| Setup       | Uses HTML template (`ngModel`)           | Uses `FormControl`, `FormGroup` in TS |
| Control     | Defined in template                      | Defined in component class            |
| Validation  | Template-based (`required`, `minlength`) | Class-based (`Validators.required`)   |
| Scalability | Simple, good for small forms             | Better for large & complex forms      |
### How do you add validations in Reactive Forms?
**Answer:**
Validations are added using validators like `Validators.required`, `Validators.minLength`, etc., in the form control or form group.
