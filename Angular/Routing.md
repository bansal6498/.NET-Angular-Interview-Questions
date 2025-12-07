## Routing
Angular Routing allows navigation between views or components in a single-page application (SPA).
#### Implentation
-   Routing is set up using RouterModule, and the paths are defined in the `app-routinh.module.ts`
-   The router links are used to define clickable navigation within templates.
```ts
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
const routes: Routes = [
    { path: '', component: HomeComponent },
    { path: 'about', component: AboutComponent }
];
@NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule]
})
export class AppRoutingModule {}
```
```html
<!-- app.component.html -->
<nav>
<a routerLink="/about">About</a>
<a routerLink="/">Home</a>
</nav>
<router-outlet></router-outlet> <!-- This is where routed components will load -->
```
### AuthGuard
AuthGuard is a service that determines if a user has permission to access a route based on their authentication status.
#### Implementation
-   Auth guards can be implemented using the `CanActivate` or `CanLoad` interfaces.
```ts
// auth.guard.ts
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from
'@angular/router';
import { Observable } from 'rxjs';
import { AuthService } from './auth.service';
@Injectable({
    providedIn: 'root'
})
export class AuthGuard implements CanActivate {
    constructor(private authService: AuthService, private router: Router) {}
    canActivate(
        next: ActivatedRouteSnapshot,
        state: RouterStateSnapshot
    ): Observable<boolean> | Promise<boolean> | boolean {
    if (this.authService.isAuthenticated()) {
        return true;
    } else {
        this.router.navigate(['/login']);
        return false;
    }
    }
}
```
#### Routing with Guard:
```ts
// app-routing.module.ts
const routes: Routes = [
{ path: 'profile', component: ProfileComponent, canActivate: [AuthGuard] }
];
```
-   **CanActivate** → Allow/deny entering a route.
-   **CanDeactivate** → Prevent leaving a route.
-   **Resolve** → Pre-fetch data before route loads.
-   **CanLoad** → Prevent lazy-loaded module loading.