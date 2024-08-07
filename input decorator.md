# @Input
Sometimes app development requires you to send data into a component. This data can be used to customize a component or perhaps send information from a parent component to a child component.

Angular uses a concept called Input. This is similar to props in other frameworks. To create an Input property, use the @Input decorator.

user.component.ts

ng g c user

from home(or) app component we shpuld pass the value and
ite recieves the value from app (or) home and display in user component

# user.component.ts

export class UserComponent {
  @Input() occupation = '';
}

# user.component.html
<p>user designation is :{{ occupation }}</p>

app.component.html

<app-user companyName="ITC Infotech"></app-user>
# @Output
When working with components it may be required to notify other components that something has happened. Perhaps a button has been clicked, an item has been added/removed from a list or some other important update has occurred. In this scenario components need to communicate with parent components.

Angular uses the @Output decorator to enable this type of behavior.



`ng g c child`
# child.component.ts
```Typescript
import { Component, inject, Output } from '@angular/core';
import { FormBuilder } from '@angular/forms';
import { EventEmitter } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-child',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './child.component.html',
  styleUrl: './child.component.scss',
})
export class ChildComponent {
  @Output() addItemEvent = new EventEmitter<any>();
  item = '';
  addItem(item: any) {
    this.addItemEvent.emit(this.item);
  }
}
```
# child.component.html
```html

<div style="background-color: burlywood">
  <input type="text" name="item" [(ngModel)]="item" />
  <button (click)="addItem()">Add Item</button>
</div>
 ```
 
ng g c parent
# parent.component.ts
```Typescript
import { Component } from '@angular/core';
import { ChildComponent } from '../child/child.component';

@Component({
  selector: 'app-parent',
  standalone: true,
  imports: [ChildComponent],
  templateUrl: './parent.component.html',
  styleUrl: './parent.component.scss',
})
export class ParentComponent {
  items: any[] = [];
  ngOnInit() {
    this.items = ['one', 'two'];
  }
  addItem(value: any) {
    this.items.push(value);
  }
}
```

# parent.component.htnml
```html
<div style="background-color: aquamarine">
  <p>parent works!</p>
  <app-child (addItemEvent)="addItem($event)"></app-child>
  <ol>
     @for( item of items;track item) {
    <li>
      {{ item }}
    </li>
    }
  </ol>
</div>
```

app.component.html
<app-parent></app-parent>