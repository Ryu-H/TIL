# Components

## Filtering a list

Angular does not provide out-of-box pipes that takes care of operations such as filtering or sorting, since 'they perform poorly and prevents aggressive minifications'. The official doc suggests that such logic to be contained in the component itself.

The steps taken in the example given out in 'Angular: Getting Started' course:
1. Another property is added to the component to hold the filtered products - if we filter the original property for products we will not be able to get back the original list of products without querying the source.
```typescript
filteredProducts: IProduct[];
products: IProduct[] = [ ... ];
```

2. The listFilter property in the ProductListComponent has been given a getter/setter pair so the setter can perform additional logic when the value is being changed from the Model Binding. The performFilter method is added
```typescript
_listFilter: string;
    get listFilter(): string {
        return this._listFilter;
    }
    set listFilter(value: string) {
        this._listFilter = value;
        this.filteredProducts = this.listFilter ? this.performFilter(this.listFilter) : this.products;
    }
    // ...
    performFilter(filterBy: string): IProduct[] {
        filterBy = filterBy.toLocaleLowerCase();
        return this.products.filter((product: IProduct) => product.productName.toLocaleLowerCase().includes(filterBy));
    }
```
3. The constructor is added for the component to set the initial values as below:
```typescript
constructor() {
  this.filteredProducts = this.products;
  this.listFilter = 'cart';
}
```
4. Don't forget to start using the filteredProducts in the template file.
```html
<tr *ngFor='let product of filteredProducts'>
<!--...-->
```
