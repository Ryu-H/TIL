# The Basics

## The Building Blocks

### Component

Angular application에서 가장 기본적으로 Logic을 나누는 단위다.

- **@angular/core** 모듈에서 임포트한 **Component** decorator로 클래스를 decorate한다.
- **Component** decorator에 Metadata를 어규먼트로 넣는다.
   - selector (html에서 reference하는 Directive가 된다)
   - template 혹은 templateUrl
- 보통 **AppComponent**가 'Root Component'가 되고 따라서 Root Component의 selector가 index.html에서 Directive로서 reference된다.
- 클래스 명은 Pascal Casing, 파일명은 app.component.ts 혹은 product-list.component.ts 같은 형태이다. (component이전에 단어들은 하이픈으로 띄어쓰는 듯)

### Module

Component들의 Logical Grouping이라고 보면 될 듯 하다. ES6의 모듈과 단어의 혼용으로 헷갈릴 수 있으니 주의.
여기서는 맥락에 따라 구분할 수 있을 것이라 생각되니 따로 구분짓지 않도록 한다.

- **AppModule**이 **AppComponent**를 가지고 있는 'Root Moodule'이 된다.
- **@angular/core** 모듈에서 **NgModule** decorator로 클래스를 decorate한다.
- imports, declarations, bootstrap의 프로퍼티를 가진 Object를 어규먼트로 넣는다. 전부 어레이임
  - import - 이 모듈이 import할 다른 모듈 - e.g. BrowserModule
  - declarations - 이 모듈이 가지고 있는 Component들
  - bootstrap - 이 모듈로 앱을 부트스트랩 할 경우 Entry-point가 되는 Component

### Template

계층상으로는 Component에 속해 있다고 봐야겠지만 실질적인 코딩상에서 작업하는 비중을 많이 차지 할 것 같아서 따로 섹션을 넣는다 (사실 그렇게 따지면 Component도 Module에 속해 있으니까 뭐)

- Component안에서 template로 inline으로 넣거나 혹은 templateUrl로 template file을 reference 한다.
- index.html이나 다른 template에서 Directive로서 어느 Component의 selector를 reference하면 그 Component의 template가 렌더링 된다.
- Angular에서 제공하는 몇몇 Directive
  - `*ngIf` - html의 attribute로 넣으면 expression이 true일 경우에만 DOM이 렌더링된다.
  - `*ngFor` - html의 attribute로 for-of 형태로 넣으면 그 array의 element수만큼 DOM이 렌더링 되고 element의 프로퍼티에 접근할 수 있다. 
