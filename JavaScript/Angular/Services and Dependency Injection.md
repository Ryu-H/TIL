# Services and Dependency Injection

## Services

Steps to building a service class is essentially similar to building a new component or a custom pipe, except we decorate with `Injectable()` decorater which is also from `'@angular/core'`. The `@Injectable` is not actually required unless the service class itself has some injected dependencies, but it is a good practice to have include it all the time.

```typescript
import { Decorator } from '@angular/core';

@Injectable()
export class ProductService() {
  getProducts(): IProduct[] {
    return [
      {
        "productId": 1,
        "productName": "Leaf Rake",
        "productCode": "GDN-0011",
        "releaseDate": "March 19, 2016",
        "description": "Leaf rake with 48-inch wooden handle.",
        "price": 19.95,
        "starRating": 3.2,
        "imageUrl": "http://openclipart.org/image/300px/svg_to_png/26215/Anonymous_Leaf_Rake.png"
      },
      // ...
    ];
  }    
}
```

## Dependency Injection

### Registering a dependency

Adding the Service class to the `providers` in either the `@Component` decorator of a component or `@NgModule` decorator of a Module will register the dependency.

Registering at a component level will allow the dependency to be injected at the component itself as well as its nested components.

Registering at Angular Module level will allow it to be injected anywhere in the application.

### Injecting dependency

The injector in Angular will inject the registered dependencies defined in the constructor of a class.

TypeScript provides a syntactic sugar for the commonly used pattern.

```typescript
  // ...
  constructor(private _productService: ProductService) {}
```
is equivalent to
```typescript
  // ...
  private _productService
  constructor(productService: ProductService) {
    this._productService = productService;
  }
```
