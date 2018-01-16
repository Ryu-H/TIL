# Routing

## Example of basic Routing definition

```typeScript
// In the Root Module

import { RouterModule } from '@angular/router';
  // ...

@NgModule({
  imports: [
    // Other modules
    RouterModule.forRoot([
      { path: 'products', component: ProductListComponent },
      { path: 'products/:id', component: ProductDetailsComponent },
      { path: 'welcome', component: WelcomeComponent },
      { path: '', redirectTo: 'welcome', pathMatch: 'full' },
      { path: '**', redirectTo: 'welcome', pathMatch: 'full' },
    ])
  ],
  // declarations, bootstrap etc
})
export class AppModule { }
```

```html
<div>
  <nav class='navbar navbar-default'>
    <div class='container-fluid'>
      <a class='navbar-brand'>{{pageTitle}}</a>
      <ul class='nav navbar-nav'>
        <li><a [routerLink]="['/welcome']">Home</a></li>
        <li><a [routerLink]="['/products']">Product List</a></li>
      </ul>
    </div>
  </nav>
  <div class='container'>
    <router-outlet></router-outlet>
  </div>
</div>
```
