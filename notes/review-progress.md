# Review progress
## 14 Apr 2021 (15, 16, 18, 20, 24, 01, 08, 15 May)
<details>
<summary>How does the data flow when using property binding?</summary>

- moves a value in one direction, from a component's property into a target element property `[prop]`

</details>

<details>
<summary>How is data binding implemented in Angular?</summary>

```TypeScript
// app/components/name/name.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  templateUrl: './name.component.html',
  styleUrls: ['./name.component.css']
})
export class NameComponent {
  title: string = 'Hello from name component!';
  name: string = 'Max';

  onButtonClick(evt: Event) {
    console.log(evt.target);
  }
}
```
```HTML
<!-- app/components/name/name.component.html -->
<!-- data-binding - communication between business logic and view -->
<!-- no multiline expressions -->
<!-- resolved to a string -->
<!-- updated dynamically at runtime -->
<!-- string interpolation -->
<p>{{ title }}</p> <!-- Hello from name component! -->
<!-- property binding -->
<p [innerText]="title"></p>
<!-- DON'T! improper usage -->
<p [innerText]="{{ title }}"></p>

<!-- event-binding - reaction to events -->
<!-- $event - browser event of type Event -->
<button type="button" (click)="onButtonClick($event)">Click</button>

<!-- two-way binding -->
<!-- triggers input data and updates BL -->
<!-- when BL is updated programmatically, updates the input -->
<!-- but have to import FormsModule on module level -->
<input type="text" [(ngModel)]="name">
<p>{{ name }}</p>
```

</details>

## 14 Apr 2021 (15, 16, 18, 20, 24, 01, 08, 15 May)
```TypeScript
// child.component.ts
import {Component, Input} from '@angular/core';

@Component({
    selector: 'app-child', // unique string '.app-class' '[appDir]'
    template: '<p></p>', // or templateUrl
    styles: ['p { color: green; }'] // or styleUrls
})
export class ChildComponent {
    @Input() lTitle: string;
    @Input('sT') sTitle: string;
}
```
```HTML
<!-- parent.component.html -->
<app-child lTitle="Some title" sT="More title"></app-child>
```