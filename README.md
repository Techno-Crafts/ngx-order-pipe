# Angular 5+ Order Pipe [![Build Status](https://travis-ci.org/VadimDez/ngx-order-pipe.svg?branch=master)](https://travis-ci.org/VadimDez/ngx-order-pipe) ![https://www.npmjs.com/package/ng2-order-pipe](https://img.shields.io/npm/dm/ng2-order-pipe.svg?style=flat) ![https://www.npmjs.com/package/ngx-order-pipe](https://img.shields.io/npm/dm/ngx-order-pipe.svg?style=flat) [![DeepScan Grade](https://deepscan.io/api/projects/1752/branches/7519/badge/grade.svg)](https://deepscan.io/dashboard/#view=project&pid=1752&bid=7519)

> Order your collection by a field

<img src="https://cloud.githubusercontent.com/assets/3748453/22164327/08764608-df57-11e6-9c90-075aeca26fd6.gif" width="300">

### Demo page
[https://vadimdez.github.io/ngx-order-pipe/](https://vadimdez.github.io/ngx-order-pipe/)

or see code example

[https://stackblitz.com/edit/angular-hmfhmx](https://stackblitz.com/edit/angular-hmfhmx?file=app%2Fapp.component.html)

## Install

```
npm install  ngx-order-pipe --save
```
*For Angular lower than 5 use version `1.1.3`*

## Setup

In case you're using `systemjs` - see configuration [here](https://github.com/VadimDez/ngx-order-pipe/blob/master/SYSTEMJS.md). Otherwise skip this part.


## Usage

##### In HTML template

```html
{{ collection | orderBy: expression : reverse : caseInsensitive : comparator }}
```

### Arguments

| Param | Type | Default | Details |
| --- | --- | --- | --- |
| collection | `array` or `object` | | The collection or object to sort |
| expression  | `string` | | The key to determinate order |
| reverse *(optional)* | `boolean`| false | Reverse sorting order |
| caseInsensitive *(optional)* | `boolean`| false | Case insensitive compare for sorting |
| comparator *(optional)* | `Function`|  | Custom comparator function to determine order of value pairs. Example: `(a, b) => { return a > b ? 1 : -1; }` [`See how to use comparator`](https://github.com/VadimDez/ngx-order-pipe/issues/39) |

Import `OrderModule` to your module

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule  } from '@angular/platform-browser';
import { AppComponent } from './app';

import { OrderModule } from 'ngx-order-pipe';

@NgModule({
  imports: [BrowserModule, OrderModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}

```

And use pipe in your component

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'example',
  template: `
    <ul>
      <li *ngFor="let item of array | orderBy: order">
        {{ item.name }}
      </li>
    </ul> 
  `
})

export class AppComponent {
  array: any[] = [{ name: 'John'} , { name: 'Mary' }, { name: 'Adam' }];
  order: string = 'name';
}
```

### Deep sorting
Use dot separated path for deep properties when passing object.
```html
<div>{{ { prop: { list: [3, 2, 1] } } | orderBy: 'prop.list' | json }}</div>
```
Result:
```html
<div>{ prop: { list: [1, 2, 3] } }</div>
```

### Use OrderPipe in the component
Import `OrderPipe` to your component:
```typescript
import { OrderPipe } from 'ngx-order-pipe';
```
Add `OrderPipe` to the constructor of your component and you're ready to use it:

```typescript
constructor(private orderPipe: OrderPipe) {
  console.log(this.orderPipe.transform(this.collection, this.order));
}
```

## License
[MIT](https://tldrlegal.com/license/mit-license) © [Vadym Yatsyuk](https://github.com/vadimdez)
