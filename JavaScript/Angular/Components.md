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

## Nested Components

We'll define components to be nestable if:
1. its template is managing only a fragment of a larger view
2. it has a selector - so it can be used as a directive rather than a Routing target
3. it optionally communicates with its container component

만든 컴퍼넌트를 Directive로 사용하기 위해선 그 컴퍼넌트를 사용될 Module의 declarations에 포함시키는 것을 잊지 않도록 하자.


### Passing Data to the Component with `@Input`

`@Input` 데코레이터로 컴퍼넌트의 프로퍼티를 데코레이트 하면 container component쪽에서 Property binding으로 nested component쪽으로 데이터를 넘길 수 있다. 튜토리얼의 Demo에선 처음에 컴퍼넌트가 `OnChanges` 인터페이스를 구현하도록 했지만 data-bound input property가 없을 경우엔 이 Lifecycle hook이 불러지지 않는 것을 확인했다.

```typescript
@Component({
  selector: 'pm-star',
  templateUrl:
})
export class StarComponent implements OnChanges {
  @Input rating: number;
  starWidth: number;
  // ...
}
```

```html
<!--from the template of container component-->
<td>
  <pm-star [rating]='product.starRating'></pm-star>
</td>
```
