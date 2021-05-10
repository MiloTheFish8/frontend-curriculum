# Angular
- [Essentials](#essentials)
- [Angular CLI](#angular-cli)
- [Initial files](#initial-files)
- [Components](#components)
- [Component Styling](#component-styling)
- [Component Lifecycle](#component-lifecycle)
- [Dynamic Components](#dynamic-components) (refactor)
- [Templates](#templates)
- [Pipes](#pipes)
- [Directives](#directives) (refactor)
- [Dependency Injection](#dependency-injection)
- [Services](#services) (refactor)
- [Router](#router) (refactor)
- [Forms: TD](#forms-template-driven) (refactor)
- [Forms: Reactive](#forms-reactive) (refactor)
- Modules (refactor)
- [Observables](#observables) (refactor)
- [Http Client](#http-client) (refactor)
- Interceptors (refactor)
- Authentication (refactor)
- Lazy loading (refactor)
- AoT Compilation (refactor)
- NgRx (refactor)
- Offline (refactor)
- Testing (refactor)
- Debugging (refactor)
- [Deploy](#deploy) (refactor)
- [Animations](#animations) (refactor)
- [PWA](#pwa) (refactor)
- [Schematics](#schematics) (refactor)
- Universal (refactor)
- Angular Elements (refactor)
- Updating Angular (refactor)
- Resources (refactor)

## Essentials
<details>
<summary>What are the core ideas behind Angular?</summary>

- components - building blocks to compose the application
- templates - cleanly separate the application's logic from its presentation
- dependency injection - allows to declare the dependencies without caring about their instantiation, write more testable and flexible code

</details>

## Angular CLI
<details>
<summary>How to create a new workspace?</summary>

```bash
# create a project
ng new <project-name>
# for multiple projects in one folder
ng new <project-name> --create-application=false
```

</details>

<details>
<summary>How to build the application?</summary>

```bash
# build for production
ng build --prod
```

</details>

<details>
<summary>How to build and serve the application?</summary>

```bash
# run the app in dev mode
ng serve
# or to specify the port
ng serve --port 3000
# to open
ng serve --open
ng serve -o
```

</details>

<details>
<summary>How to generate or modify files?</summary>

```bash
# create a component
ng g c <component-name or path + name>

# create a directive
ng g d <directive-name>

# generate one more application
ng generate application <application-name>

# generate a library
ng generate library <library-name>
```

</details>

<details>
<summary>How to run unit tests?</summary>

```bash
ng test
```

</details>

<details>
<summary>How to build, serve and run e2e tests?</summary>

```bash
ng e2e
```

</details>

<details>
<summary>How to run linter?</summary>

```bash
# check linting errors
ng lint
```

</details>

<details>
<summary>Why do you want to create a library?</summary>

- not an app to use on it's own but to use across the applications (ex Angular Material)

</details>

<details>
<summary>Learn more</summary>

- [Angular CLI Official](https://angular.io/cli)
- [Angular Compiler Options](https://angular.io/guide/angular-compiler-options)
- [Angular workspace configuration](https://angular.io/guide/workspace-config)
- [Schematics for the Angular CLI](https://angular.io/guide/schematics)

</details>

## Initial files
<details>
<summary>How to import .ts files?</summary>

- don't import with `.ts` extensions, webpack adds it

</details>

<details>
<summary>What is the entry file and how it works?</summary>

- `main.ts` is the main entry point for your application
- compiles the application with the JIT compiler (can also use the AOT compiler without changing any code by appending the `--aot` flag to the CLI build and serve commands)
- bootstraps the application's root module (`AppModule`) to run in the browser
```TypeScript
// main.ts
import {enableProdMode} from '@angular/core';
import {platformBrowserDynamic} from '@angular/platform-browser-dynamic';

import {AppModule} from './app/app.module';
import {environment} from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

</details>

<details>
<summary>What is the AppModule?</summary>

- the root (and only required) module
```TypeScript
// app/app.module.ts
import {NgModule} from '@angular/core';
import {AppComponent} from './app.component';

@NgModule({
  // should be known components when Angular analyses index.html
  bootstrap: [AppComponent]
})
export class AppModule {}
```

</details>

<details>
<summary>What is the AppComponent?</summary>

- the bootstrap (and only required) component
```TypeScript
// app/app.component.ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './'
})
export class AppComponent {}
```

</details>

<details>
<summary>How to add the app to HTML?</summary>

```HTML
<!-- index.html -->
<!doctype html>
<html>
  <head>
    <!-- ... -->
  </head>
  <body>
    <app-root></app-root>
  </body>
</html>
```

</details>

<details>
<summary>Learn more</summary>

- [Docs: File structure](https://angular.io/guide/file-structure)

</details>

## Components
<details>
<summary>What is a component?</summary>

- a TypeScript class with `@Component()` decorator, HTML template and styles
- `Component` is a type of a `Directive`

</details>

<details>
<summary>How to create a basic component?</summary>

```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';
import { NameComponent } from './components/name/name.component';

@NgModule({
  declarations: [NameComponent]
})
export class AppModule {}
```
```TypeScript
// app/components/name/name.component.ts
import { Component } from '@angular/core';

@Component({
  // required, must be a unique string
  selector: 'app-name', // tag, mostly for components
  selector: '[appDir]', // attribute, mostly for directives
  selector: '.class', // can also use a class as a selector
  // required, only one of
  template: '<p>Some text</p>',
  templateUrl: './name.component.html',
  // optional, only one of
  styles: ['p { color: orange; }'],
  styleUrls: ['./name.component.css'] // scss / less also possible
})
export class NameComponent {}
```
```HTML
<!-- app/components/name/name.component.html -->
<app-name></app-name>
<p appDir></p>
<p class="class"></p>
```

</details>

<details>
<summary>How does the data flow when using property binding?</summary>

- moves a value in one direction, from a component's property into a target element property `[prop]`

</details>

<details>
<summary>Is it secure to use property binding and string interpolation without sanitizing?</summary>

- it is safe as Angular does sanitizing by itself

</details>

<details>
<summary>What is the difference between string interpolation and property binding?</summary>

- `{{}}` converts to a string
- only prop binding is used when we need to pass the value which is not a string

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

<details>
<summary>How to pass data from parent to child with input binding?</summary>

```TypeScript
// app/components/child/child.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent {
  // to allow access from the outside
  // (by default props are accessible
  // only from the inside of the component)
  // if object = same object (reference type)
  @Input() user: object;
  @Input('fieldLabel') label: string;
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<app-child [user]="{ name: 'Lala' }" fieldLabel="E-mail"></app-child>
```

</details>

<details>
<summary>How to intercept input property changes with a setter?</summary>

```TypeScript
// app/components/child/child.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent {
  private _fieldLabel = '';
  @Input() 
  get fieldLabel(): string { return this._fieldLabel; };
  set fieldLabel(fieldLabel: string) {
    this._fieldLabel = (fieldLabel && fieldLabel.trim()) || 'Unknown Label';
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<!-- E-mail -->
<app-child fieldLabel="E-mail"></app-child>
<!-- Unknown Label -->
<app-child fieldLabel="  "></app-child>
```

</details>

<details>
<summary>How to intercept input property changes with OnChanges and why?</summary>

- you may prefer this approach to the property setter when watching multiple, interacting input properties
```TypeScript
// app/components/child/child.component.ts
import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent implements OnChanges {
  @Input() level: number;
  @Input() power: number;
  changeLog: string[] = [];

  ngOnChanges(changes: SimpleChanges) {
    const log: string[] = [];

    for (const propName in changes) {
      const changedProp = changes[propName];
      const to = JSON.stringify(changedProp.currentValue);

      if (changedProp.isFirstChange()) {
        log.push(`Initial value of ${propName} set to ${to}`)
      } else {
        const from = JSON.stringify(changedProp.previousValue);

        log.push(`${propName} changed from ${from} to ${to}`);
      }
    }

    this.changeLog.push(log.join(', '));
  }
}

// app/components/parent/parent.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  templateUrl: './'
})
export class ParentComponent {
  level: number = 1;
  power: number = 0;

  increasePower() {
    this.power++;
  }

  increaseLevel() {
    this.level++;
    this.power = 0;
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<button type="button" (click)="increasePower()">Power Up</button>
<button type="button" (click)="increaseLevel()">Level Up</button>
<app-child [level]="level" [power]="power"></app-child>
```

</details>

<details>
<summary>How to pass data from child to parent (listen to child event)?</summary>

- the child exposes an `EventEmitter` property with which it emits events when something happens
- the parent binds to that event property and reacts to those events
```TypeScript
// app/components/child/child.component.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <h2>{{ name }}</h2>
    <button 
      (click)="checkIn(true)" 
      [disabled]="haveChosen" 
      type="button"
    >Check In</button>
    <button 
      (click)="checkIn(false)" 
      [disabled]="haveChosen" 
      type="button"
    >I'm Out</button>
  `
})
export class ChildComponent implements OnChanges {
  @Input() name: string;
  @Output() checkedIn = new EventEmitter<boolean>();
  haveChosen = false;

  checkIn(isIn: boolean) {
    this.checkedIn.emit(isIn);
    this.haveChosen = true;
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<app-child name="Harry" (checkedIn)="onCheckedIn($event)"></app-child>
```

</details>

<details>
<summary>How to update values from parent to child and otherwise with 2-way data binding?</summary>

```TypeScript
// parent.component.ts
@Component({...})
export class ParentComponent {
  // sets the initial value of ChildComponent.size
  fontSizePx = 18;
}

// child.component.ts
@Component({...})
export class ChildComponent {
  // for 2-way binding to work
  // @Output() property must use inputChange pattern
  @Input() size: number;
  @Output() sizeChange = new EventEmitter<number>();

  dec() {
    this.size--;
    this.sizeChange.emit(this.size);
  }

  inc() {
    this.size++;
    this.sizeChange.emit(this.size);
  }
}
```
```HTML
<!-- parent.component.html -->
<!-- use a combination of [] and () bindings -->
<app-child [(size)]="fontSizePx"></app-child>
<!-- it's a shorthand of bindings -->
<app-child [size]="fontSizePx" (sizeChange)="fontSizePx=$event"></app-child>
<p [style.font-size.px]="fontSizePx">Resizable text</p>

<!-- child.component.html -->
<button type="button" (click)="dec()">Smaller</button>
<button type="button" (click)="inc()">Bigger</button>
<p>Font Size: {{ size }}px</p>
```

</details>

<details>
<summary>How to use a local reference (inside one component) and what is the limitation?</summary>

- can be used only in the template, not in the component (.ts file)
- returns an HTML element
```HTML
<!-- simple.component.html -->
<input type="text" #locRef>
<button (click)="onButtonClick(locRef)" type="button">Get the input HTML</button>
<p>{{ locRef.value }}</p>
```

</details>

<details>
<summary>How to interact parent > child via local variable (reference) and what is the limitation?</summary>

- parent component cannot use data binding to read child properties or invoke child methods
- can do both by creating a template reference variable for the child element and then reference that variable within the parent template
- accessible only from the template, not from the parent component itself
```TypeScript
// child.component.ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p>{{ message }}</p>'
})
export class ChildComponent {
  message: string = '';

  start() {
    this.message = 'Start in 10 seconds.';
    // some countdown code
  }

  stop() {
    this.message = 'Stopped!';
    // stop the timer code
  }
}
```
```HTML
<!-- parent.component.html -->
<app-child #childComponent></app-child>
<p>{{ childComponent.message }}</p>
<button (click)="childComponent.start()" type="button">Start</button>
<button (click)="childComponent.stop()" type="button">Stop</button>
```

</details>

<details>
<summary>How to use an @ViewChild (inside one component) and why?</summary>

- to get access to the html element from ts file
```TypeScript
// simple.component.ts
import {Component, ViewChild, ElementRef} from '@angular/core';

@Component({
  selector: 'app-simple',
  templateUrl: './'
})
export class SimpleComponent {
  // returns an element with this localRef
  // { static: true / false } (for Angular < 9)
  // true if we plan to use it inside ngOnInit()
  @ViewChild('locRef') input: ElementRef;

  getValue() {
    // don't change the value via this approach
    return this.input.nativeElement.value;
  }
}
```
```HTML
<!-- simple.component.html -->
<input type="text" #locRef>
```

</details>

<details>
<summary>How to interact parent > child via @ViewChild() and why?</summary>

- returns the first occurrence of the child component
- to be able to use child component methods and props from inside the parent component itself
- you need to use the `AfterViewInit` hook to set some initial properties
```TypeScript
// child.component.ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p>{{ message }}</p>'
})
export class ChildComponent {
  message: string = '';

  start() {
    this.message = 'Start in 10 seconds.';
    // some countdown code
  }

  stop() {
    this.message = 'Stopped!';
    // stop the timer code
  }
}

// parent.component.ts
import {Component, ViewChild, AfterViewInit} from '@angular/core';
import {ChildComponent} from './components/child/child.component';

@Component({
  selector: 'app-parent',
  templateUrl: './'
})
export class ParentComponent implements AfterViewInit {
  @ViewChild(ChildComponent) childComponent: ChildComponent;
  message: string = '';

  ngAfterViewInit() {
    // redefine message to get from child component
    // but wait a tick first to avoid one-time devMode
    // unidirectional-data-flow-violation error
    // because it's too late to update the parent view already
    // in the same cycle
    setTimeout(() => this.message = () => this.childComponent.message, 0);
  }

  start() {
    this.childComponent.start();
  }

  stop() {
    this.childComponent.stop();
  }
}
```
```HTML
<!-- parent.component.html -->
<app-child></app-child>
<p>{{ message }}</p>
<button (click)="start()" type="button">Start</button>
<button (click)="stop()" type="button">Stop</button>
```

</details>

<details>
<summary>How to use @ContentChild and why?</summary>

- to get the first element or the directive matching the selector from the content DOM
- if the content DOM changes, and a new child matches the selector, the property will be updated
- content queries are set before the `ngAfterContentInit` callback is called
- does not retrieve elements or directives that are in other components' templates, since a component's template is always a black box to its ancestors
- `static` metadata property is used to configure how we resolve the query results: `true` - before the change detection runs, `false` - default, after the change detection runs
```TypeScript
// basic example
import {AfterContentInit, ContentChild, Directive} from '@angular/core';

@Directive({
  selector: '[childDirective]'
})
export class ChildDirective {}

@Directive({
  selector: '[parentDirective]'
})
export class ParentDirective implements AfterContentInit {
  @ContentChild(ChildDirective) contentChild: ChildDirective;

  ngAfterContentInit() {
    // here the contentChild is set
  }
}
```
```TypeScript
// usage
import {Component, ContentChild, Directive, Input} from '@angular/core';

@Directive({
  selector: 'app-tab-item'
})
export class TabItem {
  @Input() label: string;
}

@Component({
  selector: 'app-tab',
  template: `<p>{{ tabItem.label }}</p>`
})
export class Tab {
  @ContentChild(TabItem) tabItem: TabItem;
}

@Component({
  selector: 'app-simple',
  template: `
    <app-tab>
      <app-tab-item *ngIf="isFirst" label="First"></app-tab-item>
      <app-tab-item *ngIf="!isFirst" label="Second"></app-tab-item>
    </app-tab>
    <button type="button" (click)="toggleTabs()">Switch Tabs</button>
  `
})
export class SimpleComponent {
  isFirst = true;

  toggleTabs() {
    this.isFirst = !this.isFirst;
  }
}
```

</details>

<details>
<summary>How to use @ContentChild with ng-content and why?</summary>

- use `<ng-content>` to project some HTML from parent into child
- don't change the value via this approach
```TypeScript
// child.component.ts
import {Component, ContentChild, ElementRef} from '@angular/core';

@Component({})
export class ChildComponent {
  // static true - before the change detection runs,
  // false - default, after the change detection runs
  // < 9 version required
  @ContentChild('locRef', {static: true}) element: ElementRef;

  doSomething() {
    // to access the html element
    this.element.nativeElement;
  }
}

// parent.component.ts
@Component({})
export class ParentComponent {}
```
```HTML
<!-- child.component.html -->
<div class="child">
  <!-- without ng-content the content from parent will be list -->
  <ng-content></ng-content>
</div>

<!-- parent.component.html -->
<app-child>
  <!-- add local reference to access from @ContentChild -->
  <p #locRef>Some text</p>
</app-child>
```

</details>

## Component Styling
<details>
<summary>What is view encapsulation and what is it for?</summary>

- basically for CSS not to affect all the other parts of the app

</details>

<details>
<summary>How to set view encapsulation?</summary>

```TypeScript
import {Component} from '@angular/core';

@Component({
  // default
  // emulates the behavior of shadow DOM 
  // by preprocessing (and renaming) the CSS code 
  // to effectively scope the CSS to the component's view
  encapsulation: ViewEncapsulation.Emulated,
  // uses the browser's native shadow DOM implementation 
  // to attach a shadow DOM to the component's host element
  // and then puts the component view inside that shadow DOM
  // the component's styles are included within the shadow DOM
  // only works on browsers that have native support for shadow DOM
  encapsulation: ViewEncapsulation.ShadowDom,
  // Angular adds the CSS to the global styles
  encapsulation: ViewEncapsulation.None
})
export class SimpleComponent {}
```

</details>

<details>
<summary>What are special selectors and how to use them?</summary>

```CSS
/* targets styles in the element that hosts the component */
/* the only way to target the host element */
/* as it's not a part of the component's template */
/* do not add selectors (other than :host-context) in front of it */
/* such selectors are not scoped to a component's view */
/* and will select the outer context, but it's not native behavior */
/* use :host-context instead */
:host {}
/* can use conditions */
:host( .current) {}
/* combine with other selectors */
:host p {}

/* to apply styles based on some condition outside of a component's view */
/* looks for a CSS class in any ancestor of the component host element, */
/* up to the document root */
/* useful when combined with another selector */
:host-context(.theme-dark) p {}

/* deep selectors are deprecated */
::ng-deep {}
>>> {}
/deep/ {}
```

</details>

<details>
<summary>How to add styles to a component?</summary>

- the scoping rules apply to all the loading patterns (except external global)
- by setting `styles` or `styleUrls` metadata
- inline in the template HTML (in `template` or `templateUrl` file)
```HTML
<!-- simple.component.html -->
<style>
  p {
    font-size: 16px;
  }
</style>
<link rel="stylesheet" href="../assets/styles/simple.css">
<p>{{ title }}</p>
```
- with CSS imports
```CSS
/* simple.component.css */
@import '../styles/simple.css';
```
- external global styles are added to `angular.json` (not scoped)

</details>

## Component Lifecycle
<details>
<summary>When does component lifecycle start?</summary>

 - when Angular instantiates the component class and renders the component view along with its child views

</details>

<details>
<summary>How does lifecycle continue?</summary>

- with change detection, as Angular checks to see when data-bound properties change, and updates both the view and the component instance as needed

</details>

<details>
<summary>When does component lifecycle end?</summary>

- when Angular destroys the component instance and removes its rendered template from the DOM

</details>

<details>
<summary>Why do you want to use lifecycle hooks?</summary>

- to initialize new instances
- initiate change detection when needed
- respond to updates during change detection
- clean up before deletion of instances

</details>

<details>
<summary>What is the Component lifecycle event sequence?</summary>

```TypeScript
export class SimpleComponent {
  // 0. before all the hooks
  constructor() {}

  // 1. and whenever one or more data-bound input properties change
  ngOnChanges(changes: SimpleChanges) {
    // object of current and previous property values
    console.log(changes);
  }

  // 2. once, after the first ngOnChanges()
  ngOnInit() {}

  // 3. immediately after ngOnChanges()
  ngDoCheck() {}

  // 4. once after the first ngDoCheck()
  ngAfterContentInit() {}

  // 5. after ngAfterContentInit() and every subsequent ngDoCheck()
  ngAfterContentChecked() {}

  // 6. once after the first ngAfterContentChecked()
  ngAfterViewInit() {}

  // 7. after the ngAfterViewInit() and every subsequent ngAfterContentChecked()
  ngAfterViewChecked() {}

  // 8. immediately before Angular destroys the directive or component
  ngOnDestroy() {}
}
```

</details>

<details>
<summary>How does ngOnChanges() work and when do you use it?</summary>

- respond when Angular sets or resets data-bound input properties
- runs only when the actual value changes (if the reference stays the same for complex data, even if the value inside changes, doesn't run)
- happens very frequently
- any operation here impacts performance significantly
- if a component has no inputs or you use it without providing any inputs, will not be called

</details>

<details>
<summary>How does ngOnInit() work and when do you use it?</summary>

- initialize the component after Angular first displays the data-bound properties and sets the component's input properties
- a good place for a component to fetch its initial data (perform complex initializations outside of the constructor - components should be cheap and safe to construct)
- set up the component after Angular sets the input properties (as the constructors should do no more than set the initial local variables to simple values)

</details>

<details>
<summary>How does ngDoCheck() work and when do you use it?</summary>

- detect and act upon changes that Angular can't or won't detect on its own
- monitor changes that occur where `ngOnChanges()` won't catch them
- extremely expensive hook - called with enormous frequency - after every change detection cycle no matter where the change occurred
- most of these initial checks are triggered by Angular's first rendering of unrelated data elsewhere on the page (just moving the cursor into another `<input>` triggers a call, relatively few calls reveal actual changes to data) 
- if you use this hook, your implementation must be extremely lightweight or the user experience suffers

</details>

<details>
<summary>How does ngAfterContentInit() work and when do you use it?</summary>

- respond after Angular projects external content into the component's view
- `@ContentChild()` prop is set after the view has been initiated
- no need to delay the update to ensure proper rendering (as we do for AfterViewInit and AfterViewChecked)
- Angular calls both AfterContent hooks before calling either of the AfterView hooks
- Angular completes composition of the projected content before finishing the composition of this component's view. There is a small window between the AfterContent... and AfterView... hooks that allows you to modify the host view

</details>

<details>
<summary>How does ngAfterContentChecked() work and when do you use it?</summary>

- respond after Angular checks the content projected into the component
- `@ContentChild()` prop is updated after the view has been checked
- no need to delay the update to ensure proper rendering (as we do for AfterViewInit and AfterViewChecked)
- Angular calls both AfterContent hooks before calling either of the AfterView hooks
- Angular completes composition of the projected content before finishing the composition of this component's view. There is a small window between the AfterContent... and AfterView... hooks that allows you to modify the host view

</details>

<details>
<summary>How does ngAfterViewInit() work and when do you use it?</summary>

- respond after Angular initializes the component's views and child views
- `@ViewChild()` prop is set after the view has been initiated

</details>

<details>
<summary>How does ngAfterViewChecked() work and when do you use it?</summary>

- respond after Angular checks the component's views and child views
- `@ViewChild()` prop is updated after the view has been checked

</details>

<details>
<summary>How does ngOnDestroy() work and when do you use it?</summary>

- cleanup just before Angular destroys the directive or component
- unsubscribe Observables and detach event handlers to avoid memory leaks
- stop interval timers
- un-register all callbacks that were registered globally or app services
- notify another part of the application that the component is going away

</details>

<details>
<summary>Learn more</summary>

- [Docs: Components](https://angular.io/guide/component-overview)
- [Docs: Introduction to components and templates](https://angular.io/guide/architecture-components)
- [Docs: Component interaction](https://angular.io/guide/component-interaction)
- [Docs: Lifecycle hooks](https://angular.io/guide/lifecycle-hooks)

</details>

## Dynamic Components
<details>
<summary>What are the dynamic components and why do you use them?</summary>

- when we need to load new components at runtime
- components which are loaded programmatically
  - declarative with `*ngIf` (better if we can use this approach)
  - programmatic with Dynamic Component Loader (mostly when we want to create some external library)
    - component created and added to DOM via code (imperatively)
    - component is added and managed by a developer

</details>

<details>
<summary>How to create and use a dynamic component?</summary>

- we can't just create a dynamic component with `new` keyword
```TypeScript
import {Component} from '@angular/component';
import {ModalComponent} from '../modal/modal.component';

@Component({
  selector: 'app-child',
  templateUrl: './'
})
export class ChildComponent {
  // is valid TS code, but not valid for angular, won't work
  // Angular does lots of things to instantiate a component 
  // (change detection in the DOM)
  // need component factory
  alertComponent = new ModalComponent();
}
```
- the right way is by using a `ComponentFactoryResolver`
1. the anchor directive - a place to attach the component
```TypeScript
// can't attach with `@ViewChild()`
// we need a viewContainerRef - object managed by Angular, 
// which gives a reference to a place in the DOM with which it can interact
import {Directive, ViewContainerRef} from '@angular/core';

@Directive({
  selector: '[appModalHost]'
})
export class ModalHostDirective {
  // inject a ViewContainerRef to gain access 
  // to the view container of the element 
  // that will host the dynamically added component
  constructor(public viewContainerRef: ViewContainerRef) {}
}
```
2. load the component with `<ng-template>` (a good choice for dynamic components because it doesn't render any additional output)
```HTML
<!-- child.component.html -->
<ng-template appModalHost></ng-template>
```
3. resolve the components
```TypeScript
import {Component, Input, ComponentFactoryResolver} from '@angular/core';
import {ModalComponent} from '../modal.component';
import {ModalDirective} from '../modal.directive';

@Component({
  selector: 'app-child',
  templateUrl: './'
})
export class ChildComponent {
  @Input() modals: string[] = ['Text 1', 'Text 2', 'Text3'];
  // will look for the 1st occurrence in the component
  // to get the access to the inner prop (viewContainerRef)
  @ViewChild(ModalDirective) appModalHost: ModalDirective;
  currentModalIndex = -1;

  constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

  loadComponent() {
    // pick the modal (just for example)
    this.currentModalIndex = (this.currentModalIndex + 1) % this.modals.length;
    const modalText = this.modals[this.currentModalIndex];
    
    // uses ComponentFactoryResolver to resolve a ComponentFactory 
    // for each specific component
    // the ComponentFactory then creates an instance of each component
    // pass the component type here
    // returns not component but component factory
    const componentFactory = this.componentFactoryResolver
      .resolveComponentFactory(ModalComponent);

    // access the point where to insert the dynamic component
    const viewContainerRef = this.appModalHost.viewContainerRef;
    // first clean all that was here before
    viewContainerRef.clear();

    // add component to the template
    // returns a reference to the loaded component
    const componentRef = viewContainerRef
      .createComponent<ModalComponent>(componentFactory);
    // access this component instance to pass the text (prop of the component)
    componentRef.instance.text = modalText;
  }
}
```

</details>

<details>
<summary>Entry Components</summary>

- error before Angular 9 (ivi has no such error) when creating the component manually
- angular checks for the component either in module declarations or in router
- but it doesn't work when we create the component manually
- have to prepare angular that it will be created at some point
```TypeScript
@NgModule({
  // ...
  // only for components, which are not created via selector <app-component>
  // or in router
  entryComponents: [
    AlertComponent
  ]
})
```

</details>

<details>
<summary>Data binding and Event binding</summary>

```TypeScript
private showErrorAlert(...) {
  // ...
  const componentRef = hostViewContainerRef.createComponent(alertComponentFactory);
  // instance has our props
  componentRef.instance.message = message;
  this.closeSub = componentRef.instance.close.subscribe(() => {
    this.closeSub.unsubscribe();
    hostViewContainerRef.clear();
  });
}

// when the upper component is destroyed
ngOnDestroy() {
  this.closeSub.unsubscribe();
}
```

</details>

<details>
<summary>Learn more</summary>

- [Dynamic component loader](https://angular.io/guide/dynamic-component-loader)

</details>

## Templates
<details>
<summary>Why is it better to use quick execution for text interpolation?</summary>

- Angular executes template expressions after every change detection cycle (many async activities trigger change detection cycles, such as promise resolutions, HTTP results, timer events, browser events)

</details>

<details>
<summary>What is attribute binding and why do we need it?</summary>

- recommended that you set an element property with a property binding whenever possible
- when you don't have an element property to bind - use attribute binding (ex: ARIA, SVG)
```HTML
<button type="button" [attr.aria-label]="Bookmark"></button>
<table>
  <tr>
    <!-- but property is colSpan -->
    <td [attr.colspan]="1 + 2">One plus two</td>
  </tr>
</table>
```

</details>

<details>
<summary>How to bind to a single or multiple classes?</summary>

```HTML
<!-- single: boolean -->
<p [class.current]="isCurrent">Item</p>
<!-- multiple: class expression -->
<!-- class string: 'class-1 class-2 class-3' -->
<!-- object: {one: true, two: false} -->
<!-- array: ['one', 'two'] -->
<p [class]="classExpression">Some text here</p>
```

</details>

<details>
<summary>How to bind to a single or multiple style attributes?</summary>

```HTML
<!-- single -->
<p [style.background-color]="colorValue">Some text here</p>
<p [style.backgroundColor]="colorValue">Some text here</p>
<!-- string: 100px -->
<p [style.width]="widthValue"></p>
<!-- number: 100 -->
<p [style.width.px]="widthValue"></p>
<!-- multiple: style expression -->
<!-- string: 'width: 100px; height: 100px;' -->
<!-- object: {width: '100px', backgroundColor: 'blue'} -->
<!-- in case of an object, have to change the link to the object -->
<!-- otherwise Angular won't update the styles (change detection) -->
<p [style]="styleExpression">Some text</p>
```

</details>

<details>
<summary>How does the style precedence work?</summary>

- the more specific a class or style binding is, the higher its precedence
- `[class.foo]` is higher than `[class]`, the same for the `[style]`
- template bindings are the most specific because they apply to the element directly and exclusively
- directive host bindings are less specific because directives can be used in multiple locations, so they have a lower precedence than template bindings
- directives often augment component behavior, so host bindings from components have the lowest precedence
- bindings take precedence over static attributes `[class]` is higher than `class` just because it's dynamic
```HTML
<!-- `class.special` template binding -->
<!-- overrides any host binding to the `special` class  -->
<!-- set by `appDir` or `app-child`-->
<app-child [class.special]="isSpecial" appDir>Text here</app-child>
<!-- same here but with the property -->
<app-child [style.color]="color" appDir>Text here</app-child>
```
- it is possible for higher precedence styles to "delegate" to lower precedence styles using undefined values (setting a style property to null ensures the style is removed, setting to undefined will cause Angular to fall back to the next-highest precedence binding to that style)
```HTML
<!-- if both app-child and appDir have [style.width] host binding -->
<!-- if appDir sets it to undefined - fallback to width set in app-child -->
<!-- if appDir sets to null - width prop will be removed -->
<app-child appDir></app-child>
```

</details>

<details>
<summary>How to pass the value of an HTML attribute to a component or directive constructor?</summary>

```TypeScript
// the injected value captures 
// the value of the specified HTML attribute at that moment
// future updates to the attribute value 
// are not reflected in the injected value
import {Attribute, Component} from '@angular/core';

@Component({
  selector: 'app-button',
  template: '<button></button>'
})
export class ButtonComponent {
  constructor(@Attribute('type') public type: string) {}
}
```
```HTML
<app-button type="submit"></app-button>
```

</details>

<details>
<summary>What is the difference in usage between @Input and @Attribute?</summary>

- use `@Input()` when you want to keep track of the attribute value and update the associated property
- use `@Attribute()` when you want to inject the value of an HTML attribute to a component or directive constructor

</details>

<details>
<summary>What is a template variable (local reference in the component section) and to what can it refer?</summary>

- helps to use data from one part of a template in another part of the template
- can refer to the following:
  - a DOM element within a template
  - a directive
  - an element
  - TemplateRef
  - a web component

</details>

<details>
<summary>How does Angular assign the value to the template variable?</summary>

- based on where you declare the variable:
  - if on a component - refers to the component instance
  - if on a standard HTML tag - refers to the element
  - if on an `<ng-template>` element - refers to a `TemplateRef` instance, which represents the template
  - if the variable specifies a name on the right-hand side, such as `#var="ngModel"` - refers to the directive or component on the element with a matching `exportAs` name (there is a difference between a `Component` and a `Directive`: Angular references a `Component` without specifying the attribute value, and a `Directive` does not change the implicit reference, or the element)

</details>

<details>
<summary>How to use NgForm with template variables (and why not just the reference to the html element)?</summary>

```HTML
<!-- the NgForm directive reference as exportAs name -->
<!-- have to specify the directive (unlike Component) -->
<form #subForm="ngForm" (nfSubmit)="onSubmit(subForm)">
  <label for="name">Name:</label>
  <input id="name" name="name" type="text" ngModel>
  <button type="submit">Submit</button>
</form>
<!-- with NgForm, subForm is a reference to the NgForm directive -->
<!-- available to track the value and validity of every control -->
<!-- unlike the native <form> element, -->
<!-- the NgForm directive has a form property -->
<!-- allows to react when the form is not valid -->
<p [hidden]="!subForm.form.valid">{{ errorMessage }}</p>
```

</details>

<details>
<summary>What is the template variable scope?</summary>

- can refer to a template variable anywhere within its surrounding template
- structural directives, such as `*ngIf` and `*ngFor`, or `<ng-template>` act as a template boundary
- cannot access template variables outside of these boundaries
```HTML
<!-- inner template can access outer variables -->
<input type="text" #locRef>
<p *ngIf="isFilled">{{ locRef.value }}</p>
<!-- here there is an implied <ng-template> around the <p> -->
<!-- and the definition of the variable is outside of it -->
<!-- accessing a template variable from the parent template works -->
<!-- because the child template inherits the context from the parent template -->
<ng-template [ngIf]="isFilled">
  <p>{{ locRef.value }}</p>
</ng-template>

<!-- but outer template can't access the inner -->
<input *ngIf="isFilled" type="text" #locRef>
<!-- doesn't work -->
<p>{{ locRef.value }}</p>
<!-- because if we rewrite it -->
<ng-template [ngIf]="isFilled">
  <!-- the ref is defined inside a template -->
  <input type="text" #locRef>
</ng-template>

<!-- the same is true for ngFor -->
<ng-container *ngFor="let item of [1, 2, 3]">
  <input type="text" #locRef>
</ng-container>
<!-- the structural directive *ngFor instantiates the template n times -->
<!-- it is impossible to define what the locRef.value is -->
<!-- doesn't work -->
<p>{{ locRef.value }}</p>

<!-- with structural directives, such as *ngFor or *ngIf, -->
<!-- there is no way for Angular to know -->
<!-- if a template is ever instantiated -->
<!-- Angular isn't able to access the value and returns an error -->
```

</details>

<details>
<summary>How to access a template variable within <ng-template> (and get the TemplateRef?</summary>

```HTML
<ng-template #templateRef></ng-template>
<button (click)="log(templateRef)">Log the #templateRef</button>
<!-- the value output is TemplateRef function -->
<!-- f TemplateRef() -->
<!-- name: 'TemplateRef' -->
<!-- __proto__: Function -->
```

</details>

<details>
<summary>What is a template input variable and how is it different to template variable?</summary>

- you can reference it within a single instance of the template, declared using `let` keyword `let item`
- scope is limited to a single instance of the repeated template (can use the same variable name again in the definition of other structural directives)
- in contrast, you declare a template variable by prefixing the variable name with `#` - `#var`, a template variable refers to its attached element, component, or directive
- template input variables and template variables names have their own namespaces (`let item` is not the same variable as `#item`)

</details>

<details>
<summary>How to use SVG as a template?</summary>

- the same as HTML templates
- able to use directives and bindings just like with HTML templates
- can create dynamic interactive graphics
```TypeScript
// rectangle-svg.component.ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-rectangle-svg',
  templateUrl: './rectangle-svg.component.svg',
  styleUrls: ['./']
})
export class RectangleSvgComponent {
  fillColor = 'green';

  changeColor() {}
}
```
```HTML
<!-- rectangle-svg.component.svg -->
<svg>
  <rect 
    x="0" y="0" 
    width="100" height="100" 
    [attr.fill]="fillColor" 
    (click)="changeColor()"
  />
</svg>
```

</details>

<details>
<summary>Learn more</summary>

- [Docs: Templates](https://angular.io/guide/template-syntax)
- [Docs: Introduction to components and templates](https://angular.io/guide/architecture-components)

</details>

## Pipes
<details>
<summary>Why and how to use pipes?</summary>

- to transform a value in the template (output) sync/async data
- used inside the template
- can be used on any output, even on `*ngFor` loop items

</details>

<details>
<summary>How to use built-in pipes?</summary>

```TypeScript
{{ data | uppercase }}
// with parameters (for multiple date:param1:param2)
{{ new Date() | date:'fullDate' }}
// chaining, from left to right, order matters
{{ new Date() | date | uppercase }}
```

</details>

<details>
<summary>How to create a simple custom pipe?</summary>

- add to module `declarations: [ShortenPipe]`
- `{{ name | shorten }}` usage in template
- `{{ name | shorten:10 }}` usage in template with params
```TypeScript
// shorten.pipe.ts
import {Pipe, PipeTransform} from '@angular/core';

@Pipe({
  // camel case
  name: 'shorten'
})
// not necessary, but good practice to implement interface
export class ShortenPipe implements PipeTransform {
  // without params
  transform(value: any) {
    if (value.length > 10) {
      return value.substr(0, 10) + '...';
    }

    return value;
  }

  // with params
  transform(value: any, limit: number) {
    if (value.length > limit) {
      return value.substr(0, limit) + '...';
    }

    return value;
  }
}
```

</details>

<details>
<summary>What's the difference between change detection and change detection for pipes (pure)?</summary>

- change detection
  - Angular looks for changes to data-bound values in a change detection process that runs after every DOM event: every keystroke, mouse move, timer tick, and server response
  - ex: Angular updates the display every time the user adds, changes or removes a recipe
- executing a pipe to update the display with every change would slow down your app's performance
  - Angular uses a faster change-detection algorithm for executing a pipe
  - by default pipes are defined as pure
  - a pure pipe must use a pure function
  - Angular executes the pipe only when it detects a pure change to the input value (change to a primitive input value or a changed object reference)
  - Angular ignores changes within composite objects, such as a newly added element of an existing array, because checking a primitive value or object reference is much faster than performing a deep check for differences within objects
  - Angular can quickly determine if it can skip executing the pipe and updating the view
  -  if you mutate the input array, the pure pipe doesn't execute, if you replace the input array, the pipe executes and the display is updated
</details>

<details>
<summary>How to create an impure pipe (for mutated objects)?</summary>

- Angular executes an impure pipe every time change detection runs for a component (with every keystroke or mouse movement)
- long-running impure pipe could dramatically slow down your app
```HTML
<input type="text" [(ngModel)]="filteredStatus">
<ul *ngFor="let server of servers | filter:filteredStatus:'status'">
  <li>...</li>
</ul>
```

```TypeScript
// filter.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter',
  pure: false
})
export class FilterPipe implements PipeTransform {
  transform(value: any, filterString: string, propName: string): any {
    if (value.length === 0 || filterString === '') {
      return value;
    }

    const resultArray = [];

    for (const item of value) {
      if (item[propName] === filterString) {
        resultArray.push(item);
      }
    }

    return resultArray;
  }
}
```

</details>

<details>
<summary>Why is it good to use an async pipe?</summary>

- without this pipe, your component code would have to subscribe to the observable to consume its values, extract the resolved values, expose them for binding, and unsubscribe when the observable is destroyed in order to prevent memory leaks

</details>

<details>
<summary>What does async pipe do and how to stop it?</summary>

- accepts an observable (but also works with promises, async code) as input and subscribes to the input automatically
- an impure pipe that returns the latest value from a stream of data and continues to do so for the life of a given component
- when Angular destroys that component, the async pipe automatically stops

</details>

<details>
<summary>How to use an async pipe?</summary>

```TypeScript
import {Component} from '@angular/core';

@Component({
  selector: 'app-child',
  templateUrl: './'
})
export class ChildComponent {
  appStatus: Promise = new Promise((resolve, reject) => setTimeout(() => {
    resolve('stable');
  }, 3000));
}
```
```HTML
<!-- [object Object] as Angular doesn't watch the Promise automatically -->
<!-- so have to use a pipe -->
<p>{{ appStatus }}</p>
<!-- '' and changes to 'stable' -->
<!-- async pipe automatically subscribes -->
<p>{{ appStatus | async }}</p>
```

</details>

<details>
<summary>How to create a custom async pipe to cache the HTTP requests?</summary>

```TypeScript
import {HttpClient} from '@angular/common/http';
import {Pipe, PipeTransform} from '@angular/core';

@Pipe({
  name: 'fetchData',
  pure: false
})
export class FetchDataPipe implements PipeTransform {
  private cachedData: any = null;
  private cachedUrl = '';

  constructor(private http: HttpClient) {}

  transform(url: string): any {
    if (url !== this.cachedUrl) {
      this.cachedData = null;
      this.cachedUrl = url;
      this.http.get(url)
        .subscribe(result => this.cachedData = result);
    }

    return this.cachedData;
  }
}
```
```HTML
<!-- simple.component.html -->
<p>{{ 'mocks/data.json' | fetchData }}</p>
```

</details>

<details>
<summary>How to work with pipes and ternary operator?</summary>

- `|` has higher precedence than `?:` so use `(condition ? a : b) | uppercase`

</details>

<details>
<summary>Learn more</summary>

- [Docs: AsyncPipe](https://angular.io/api/common/AsyncPipe)

</details>

## Directives
<details>
<summary>What is a Directive?</summary>

- class that adds additional behavior to the elements in the Angular app

</details>

<details>
<summary>What are the types of directives?</summary>

- `Component` - most common, directive with a template
- `Attribute` - changes the appearance or behavior of an element, component, or another directive
- `Structural` — changes the DOM layout by adding and removing DOM elements

</details>

<details>
<summary>What are the built-in attribute directives?</summary>

- listen to and modify the behavior of other HTML elements, attributes, properties, and components
- look like a normal HTML attribute
- doesn't change the DOM
- event and data bindings are possible
- multiple on one element
- many NgModules (like `RouterModule` and `FormsModule`) define their own arrtibute directives
- the most common are
```TypeScript
import {Component} from '@angular/core';

@Component({
  selector: 'app-child',
  templateUrl: './'
})
export class ChildComponent {
  currentClasses = {};
  currentStyles = {};

  setCurrentClasses() {
    // sets initially ones and adda/removes classes
    // when the props change
    this.currentClasses = {
      modified: this.isChanged,
      special: this.isSpecial,
      current: this.isCurrent
    };
  }

  setCurrentStyles() {
    this.currentStyles = {
      'text-decoration': this.isCurrent ? 'underline overline' : 'none',
      'background-color': this.isSpecial ? 'green' : 'transparent'
    };
  }
}
```
```HTML
<!-- NgClass adds and removes classes -->
<!-- for a single class, better to use `[class]` binding -->
<p [ngClass]="isCurrent ? 'current' : ''">Current active here</p>
<p [ngClass]="{'class-name': boolean}">Some text here</p>
<p [ngClass]="{className: boolean}">Some text here</p>
<p [ngClass]="currentClasses">Some text here</p>
<!-- NgStyle adds and removes styles -->
<!-- better to use `[style]` binding, -->
<!-- in the future `ngStyle` might be removed -->
<p [ngStyle]="{'background-color': 'prop'}">Some text here</p>
<p [ngStyle]="{backgroundColor: 'prop'}">Some text here</p>
<p [ngStyle]="currentStyles">Some text here</p>
```

</details>

<details>
<summary>What are structural built-in directives?</summary>

- responsible for HTML layout - shape or reshape the DOM's structure, typically by adding, removing, and manipulating the host elements to which they are attached
- looks like a normal HTML attribute with a leading `*`
- affects DOM (elements get added or removed)
- can't use multiple on one element (error!)
- the most common are
```HTML
<!-- NgIf - apply to a host element -->
<!-- false - Angular removes the element from the DOM -->
<!-- then disposes of the component to free up the memory -->
<!-- and all the descendants and sub-components -->
<app-child *ngIf="isLoading"></app-child>
<!-- NgFor - repeat a node for each item in a list -->
<!-- 1. stores each item in the local looping variable -->
<!-- 2. makes each item available to the templated HTML for each iteration -->
<!-- 3. 'let item of items' => <ng-template> around the host element -->
<!-- 4. repeats <ng-template> for each item -->
<!-- index is optional -->
<p *ngFor="let item of items; let i = index">{{ item }}</p>
<!-- NgSwitch - a set of 3 directives to switch among alternative views -->
<div [ngSwitch]="hero.role">
  <app-role-healer *ngSwitchCase="'healer'" [item]="hero"></app-role-healer>
  <app-role-dd *ngSwitchCase="'dd'" [item]="hero"></app-role-dd>
  <app-role-unknown *ngSwitchDefault [item]="hero"></app-role-unknown>
</div>
```

</details>

<details>
<summary>How to use an *ngIf directive?</summary>

- if directive
  - `*ngIf="boolean; else noServer"` else is optional
  - `<ng-template #noServer>` to use else
```TypeScript
// app/components/example/example.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html'
})
export class ExampleComponent {
  canEdit = false;

  onEditClick() {
    this.canEdit = !this.canEdit;
  }
}
```
```HTML
<button type="button" (click)="onEditClick()">Edit</button>
<div *ngIf="canEdit; else noEdit">
  <p>You can edit the text!</p>
</div>
<ng-template #noEdit>
  <p>Click Edit to enable edit!</p>
</ng-template>
<p [contentEditable]="canEdit">Text to edit is here.</p>
```

</details>

<details>
<summary>How and why to track items with NgFor?</summary>

- to reduce the number of calls your app makes to the server
- with `trackBy` Angular can change and re-render only those items that have changed, rather than reloading the entire list of items
```TypeScript
import {Component} from '@angular/core';
import {Item} from './';

@Component({})
export class ChildComponent {
  // add a method to the component 
  // that returns the value NgFor should track
  // here the value to track is the item's id
  // if the browser has already rendered id, 
  // Angular keeps track of it 
  // and doesn't re-query the server for the same id
  trackByItems(index: number, item: Item): number {
    return item.id;
  }
}
```
```HTML
<p *ngFor="let item of items; trackBy: trackByItems">
  {{ item.name }}
</p>
```

</details>

<details>
<summary>How to use both NgIf and NgFor together?</summary>

- add `*ngIf` on a container element that wraps an `*ngFor` element
- one or both elements can be an `<ng-container>` not to add the extra level of HTML

</details>

<details>
<summary>How to host a directive without a DOM element?</summary>

- in Angular `<ng-container>` - grouping element that doesn't interfere with styles or layout because Angular doesn't put it in the DOM
- use when you don't need an additional wrapping HTML
```HTML
<p>
  The hero name is {{ name }}
  <ng-container *ngIf="age">
    and the age is {{ age }}
  </ng-container>
  .
</p>
<!-- or to conditionally exclude the option -->
<select>
  <ng-container *ngFor="let r of roles">
    <ng-container *ngIf="r !== 'healer'">
      <option [value]="r">{{ r }}</option>
    </ng-container>
  </ng-container>
</select>
```

</details>

<details>
<summary>How to deactivate the Angular processing for some elements?</summary>

- to prevent expression evaluation use `ngNonBindable` on the host element
- deactivates interpolation, directives and binding in templates
- stops binding for the element's child but still allows to work with the host element
```HTML
<p ngNonBindable>Will look as is: {{ 2 + 4 }}</p>
<p ngNonBindable appHighlight="green"]>
  Will look as is but green: {{ 2 + 4 }}
</p>
```

</details>

<details>
<summary>How to build an attribute directive?</summary>

```TypeScript
// highlight.directive.ts
import {Directive, ElementRef, Renderer2, OnInit} from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective implements OnInit {
  // ElementRef grants the direct access to the host DOM element
  // to which we apply appHighlight directive
  // inject the reference in the constructor
  constructor(private element: ElementRef, private renderer: Renderer2) {}

  ngOnInit() {
    // to access directly, but in some cases could not yet get rendered
    this.element.nativeElement.style.backgroundColor = 'green';
  }

  doSomething() {
    // renderer is better (inject Renderer2)
    // flags like !important, etc
    this.renderer.setStyle(this.element.nativeElement, 'color', 'green', ~flags);
  }
}
```
```HTML
<!-- any component -->
<!-- Angular creates an instance of the HighlightDirective class -->
<!-- and injects a reference to the <p> element  -->
<!-- into the directive's constructor, which sets the <p> element's  -->
<!-- background style to green -->
<p appHighlight>Highlighted text</p>
```

</details>

<details>
<summary>How to handle user events in a directive?</summary>

```TypeScript
import {Directive, ElementRef, HostListener} from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  // add events to handle
  // works like adding an event listener on the element with appHighlight
  @HostListener('mouseenter') onMouseEnter(evt: Event) {
    this.highlight('green');
  }

  @HostListener('mouseleave') onMouseLeave(evt: Event) {
    this.highlight(null);
  }

  constructor(private element: ElementRef) {}

  private highlight(color: string) {
    this.element.nativeElement.style.backgroundColor = color;
  }
}
```
```HTML
<p appHighlight>Highlight on hover</p>
```

</details>

<details>
<summary>How to add the custom property binding to a directive?</summary>

```TypeScript
import {Directive, ElementRef, Input} from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  // to use one prop with the same name
  @Input() appHighlight: string;
  @Input('appHighlight') defaultColor: string;
  // or different name
  @Input() color: string;

  constructor(private element: ElementRef) {}
}
```
```HTML
<!-- when the name of the prop is the same -->
<!-- applies the directive to the element -->
<!-- sets the color with a prop binding -->
<p [appHighlight]="'green'">Green text</p>
<p appHighlight="green">Green text</p>
<!-- when the name of the prop is not the same -->
<p appHighlight="green" color="blue">Green text</p>
```

</details>

<details>
<summary>Binding custom</summary>

```HTML
<!-- if not the same name for the prop -->
<p appDirName defaultColor="blue">
<!-- when the name of the prop is the same -->
<p [appDirName]="'blue'">
```
```TypeScript
import {Renderer2, HostBinding, OnInit} from '@angular/core';

@Directive({
  selector: '[appDirName]'
})
export class SomeDirective implements OnInit {
  // to bind to a custom property
  @Input() defaultColor: string = 'transparent';
  // to bind to the same name as a directive selector
  @Input('appDirName') defaultColor: string = 'transparent';
  // have to set initial color not to get an error
  @HostBinding('style.backgroundColor') backgroundColor: string = transparent;
  // won't work on init
  @HostBinding('style.backgroundColor') backgroundColor: string = this.defaultColor;
  

  constructor(private renderer: Renderer2) {}

  // have to set color here to work on init
  ngOnInit() { this.backgroundColor = this.defaultColor; }
}
```

</details>

<details>
<summary>How does structural directive shorthand actually work?</summary>

```HTML
<p class="name" *ngIf="player">{{ player.name }}</p>
<!-- Angular transforms * into an <ng-template> -->
<!-- that wraps the host element and its children -->
<ng-template [ngIf]="player">
  <p class="name">{{ player.name }}</p>
</ng-template>
<!-- Angular doesn't create a real <ng-template> element -->
<!-- instead rendering only the host and a comment node placeholder -->
<!--bindings={
  "ng-reflect-ng-if": "[object Object]"
}-->
<p class="name" _ngcontent-c1>Harry Potter</p>

<!-- NgFor conversion -->
<p
  *ngFor="let p of players; let i = index; let odd = odd; trackBy: trackById"
  [class.odd]="odd"
>
  {{ i }} - {{ p.name }}
</p>
<!-- converted into -->
<!-- let declares a template input variable scoped within the template -->
<!-- ex: p, i, odd - the parser translates let p, let i, let odd -->
<!-- into variables named let-p let-i let-odd -->
<!-- Angular sets i and odd to -->
<!-- the current value of the context's index and odd properties -->
<!-- the parser applies PascalCase to all directives -->
<!-- and prefixes them with directive's attribute name (here ngFor) -->
<!-- of => ngForOf; trackBy => ngForTrackBy -->
<!-- NgFor directive loops through the list -->
<!-- sets and resets properties of its own context object -->
<!-- these properties can include but not limited to -->
<!-- index, odd and a special $implicit property -->
<!-- Angular sets let-p to the value of the context's $implicit prop -->
<!-- which NgFor has initialized with the p for the current iteration -->
<ng-template
  ngFor let-p [ngForOf]="players" let-i="index" let-odd="odd"
  [ngForTrackBy]="trackById"
>
  <p [class.odd]="odd">{{ i }} - {{ p.name }}</p>
</ng-template>
```

</details>

<details>
<summary>How to create a custom structural directive?</summary>

```TypeScript
// unless.directive.ts
import {Directive, Input, ViewContainerRef, TemplateRef} from '@angular/core';

@Directive({
  selector: '[appUnless]'
})
export class UnlessDirective {
  hasView = false;
  // name is the same as a selector
  @Input() set appUnless(condition: boolean) {
    if (!condition && !this.hasView) {
      // if the condition is falsy and Angular hasn't created the view 
      // the setter causes the view container 
      // to create the embedded view from the template
      this.vcRef.createEmbeddedView(this.templateRef);
      this.hasView = true;
    } else if (condition && this.hasView) {
      // if the condition is truthy and the view is currently displayed, 
      // the setter clears the container, which disposes of the view
      this.vcRef.clear();
      this.hasView = false;
    }
  }

  // inject TemplateRef and ViewContainerRef
  constructor(
    // helps to get the <ng-template>
    private templateRef: TemplateRef<any>,
    // accesses the view container 
    private vcRef: ViewContainerRef,
  ) {}
}
```
```HTML
<!-- creates an embedded view from the Angular-generated <ng-template> -->
<!-- and inserts the view in a view container -->
<!-- adjacent to the directive's original host element (here p) -->
<p *appUnless="condition">Show this text unless the condition is true</p>
```

</details>

<details>
<summary>How to improve template type checking for custom directives?</summary>

- by adding template guard properties to the directive definition
- these properties help the Angular template type checker to find mistakes in the template at the compile time
- a prop `ngTemplateGuard_(someInputProperty)` lets to specify a more accurate type for an input expression within the template
- the `ngTemplateContextGuard` static prop declares the type of the template context

</details>

<details>
<summary>Learn more</summary>

- [Docs: Built-in directives](https://angular.io/guide/built-in-directives)
- [Docs: Structural directives](https://angular.io/guide/structural-directives)

</details>

## 6 - Models
<details>
<summary>Usage</summary>

- `recipe.model.ts` and `RecipeModel` naming
- no decorator, just a simple class
- works like a blueprint
- props creation (2 ways)
  - `constructor(public name: string) {}` shortcut, provided by TypeScript
  - ```TypeScript
    public name: string;
    constructor(name: string) { this.name = name }
    ```

</details>

## Dependency Injection
<details>
<summary>What is a dependency?</summary>

- services or objects that a class needs to perform its function

</details>

<details>
<summary>What is a Dependency Injection?</summary>

- a design pattern where a class requests dependencies from external sources rather than creating them

</details>

<details>
<summary>How and why Angular uses DI?</summary>

- provides the dependencies to a class upon instantiation
- increases flexibility and modularity of the application

</details>

<details>
<summary>What is a Dependency provider?</summary>

- by configuring providers you can make services available to the parts of your application
- configures an injector with a DI token which that injector uses to provide the runtime version of a dependency value

</details>

<details>
<summary>How to specify a provider token?</summary>

- if you specify the service class as the provider token, by default injector instantiates that class with `new`
```TypeScript
// the Logger class provides a Logger instance
providers: [Logger]
```

</details>

<details>
<summary>What is a DI token?</summary>

- when you configure an injector with a provider, you are associating that provider with a DI token
- the injector allows Angular to create a map of any internal dependencies
- the DI token acts as a key to that map
- the dependency value is an instance and the class type serves as a lookup key
```TypeScript
// the injector uses the LoggerService type as the token
// for looking up the loggerService
loggerService: LoggerService;
// when you define a constructor parameter with the LoggerService class type,
// Angular knows to inject the service 
// associated with that LoggerService class token
constructor(loggerService: LoggerService) {}
```

</details>

<details>
<summary>How to define a provider?</summary>

- the class provider syntax is a shorthand (expands into a provider config defined by the `Provider` interface)
```TypeScript
provides: [Logger]
// expands into a full provider object
// provide holds the token 
// (for locating a dependency value and configuring the injector)
// the second parameter is a provider definition object
// tells the injector how to create the dependency value
[{provide: Logger, useClass: Logger}]
```

</details>

<details>
<summary>How to specify a different class as a provider?</summary>

```TypeScript
provides: [Logger]
// using the Logger token to create a BetterLogger instance
[{provide: Logger, useClass: BetterLogger}]
```

</details>

<details>
<summary>What can you use to define the provider?</summary>

- service class
- substitute class
- an object
- a factory function

</details>

<details>
<summary>How to create an injectable service?</summary>

```JavaScript
// app/logger.service.ts
import {Injectable} from '@angular/core';

// specifies that Angular can use this class in the DI system
// 'root' - visible throughout the application
@Injectable({providedIn: 'root'})
export class LoggerService {
  doSomething() {}
}
```
```JavaScript
// app/components/hello/hello.component.ts
import {Component} from '@angular/core';
import {LoggerService} from '../../../logger.service';

@Component({
  selector: 'app-hello',
  template: '<p>Hello!</p>'
})
export class HelloComponent {
  // injecting makes the service visible to a component
  // specify the type and metadata - Angular can inject the correct service
  constructor(private loggerService: LoggerService) {}

  onLog() {
    this.logger.doSomething();
  }
}
```

</details>

<details>
<summary>Learn more</summary>

- [Docs: Dependency injection in Angular](https://angular.io/guide/dependency-injection)

</details>

## Services
<details>
<summary>What is a service in Angular?</summary>

- an instance of a class that you can make available to any part of your application using Angular's dependency injection system

</details>

<details>
<summary>How to create a service?</summary>

```TypeScript
// simple.service.ts
import {Injectable} from '@angular/core';

// with 'root' provided on the app level
@Injectable({providedIn: 'root'})
export class SimpleService {}

// app.module.ts
// to provide on the app level in module
import {NgModule} from '@angular/core';
import {SimpleService} from './simple.service';

@NgModule({})
export class AppModule {
  providers: [SimpleService]
}
```

</details>

<details>
<summary>What are the common use cases for the service?</summary>

- for less connection between app parts
- working with data
- DRY
- centralize functionality
```TypeScript
// simple.service.ts
import {Injectable} from '@angular/core';

@Injectable({providedIn: 'root'})
export class SimpleService {
  items = [];

  addItem(item) {
    this.items.push(item);
  }

  getItems() {
    return this.items;
  }

  clearItems() {
    this.items = [];
    return this.items;
  }
}
```

</details>

<details>
<summary>How to use a service?</summary>

```TypeScript
// components/basic.component.ts
import {Component} from '@angular/core';
// import the service
import {SimpleService} from '../simple.service.ts';

@Component({})
export class BasicComponent {
  // inject the service
  constructor(private simpleService: SimpleService) {}

  addNewItem(item) {
    this.simpleService.addItem(item);
  }
}
```

</details>

<details>
<summary>Usage, hierarchical injector</summary>

- NOT! `const loggingService = new LoggingService();` Angular has better way (hierarchical dependency injector)
  - injects dependency into our component automatically
  - `constructor(private logService: LoggingService) {}` to inform Angular that we require such an instance, type is required
- hierarchical dependency injector levels
  - module level - the highest: services, components
  - root component level - components
  - component level - current components and all the children
  - lower levels override higher (create a new instance of a service)

</details>

<details>
<summary>Usage strategies</summary>

- AppModule => app-wide (same instance) === {providedIn: 'root'} => root injector => use by default
- Component => component-tree (new instance) => component specific injector => use if needed
- Eager-loaded modules => app-wide, but if included into both AppModule and LazyModule === new instance! => root injector / child injector => never use, unexpected issues
- Lazy-loaded module => module-lazy-wide (new instance) => child injector => use only when needed

</details>

<details>
<summary>In other services</summary>

1. provide on module level
  - `providers: [LoggingService]` in app.module 
  - `@Injectable({ provideIn: 'root' })` inside the service, also for lazy load (Angular 6+)
2. import the service
3. `constructor(private loggingService: LoggingService) {}`
4. `@Injectable()` to allow injecting a service

</details>

<details>
<summary>How to communicate between parent and child component via service?</summary>

- service interface provides bi-directional communication for parent and child
- you can use it for parent-child scope (if you don't want to access this service from the other components) or provide on the root level
```TypeScript
// simple.service.ts
import {Injectable} from '@angular/core';
import {Subject} from 'rxjs';

@Injectable({providedIn: 'root'})
export class SimpleService {
  private level = 0;
  // Observable source
  private levelIncreasedSource = new Subject<number>();
  // Observable stream
  levelIncreased$ = this.levelIncreasedSource.asObservable();
  // Service command
  increaseLevel(level: number) {
    this.level += level;
    this.levelIncreasedSource.next(this.level);
  }
}

// child.component.ts
import {Component, OnInit, OnDestroy} from '@angular/core';
import {Subscription} from 'rxjs';
import {SimpleService} from '../simple.service';

@Component({
  selector: 'child-component',
  templateUrl: './'
})
export class ChildComponent implements OnInit, OnDestroy {
  history: number[] = [];
  subscription: Subscription;

  constructor(private simpleService: SimpleService) {}

  ngOnInit() {
    this.subscription = simpleService.levelIncreased$.subscribe(level => {
      history.push(level);
    });
  }

  ngOnDestroy() {
    this.subscription.unsubscribe();
  }

  changeLevel () {
    const level = Math.floor(Math.random() * 10);
    this.simpleService.increaseLevel(level);
  }
}

// parent.component.ts
import {Component, OnInit, OnDestroy} from '@angular/core';
import {Subscription} from 'rxjs';
import {SimpleService} from '../simple.service';

@Component({
  selector: 'app-parent',
  templateUrl: './'
})
export class ParentComponent implements OnInit, OnDestroy {
  subscription: Subscription;
  level: number;

  constructor(private simpleService: SimpleService) {}

  ngOnInit() {
    this.subscription = simpleService.levelIncreased$.subscribe((level) => {
      this.level = level;
    });
  }

  ngOnDestroy() {
    this.subscription.unsubscribe();
  }
}
```
```HTML
<!-- child.component.html -->
<button (click)="changeLevel()" type="button">Change Level</button>
<ul>
  <li *ngFor="let event of history">{{ event }}</li>
</ul>

<!-- parent.component.html -->
<app-child></app-child>
<p>Current level is {{ level | async }}</p>
```

</details>

<details>
<summary>Learn more</summary>

- [Docs: Introduction to services and dependency injection](https://angular.io/guide/architecture-services)

</details>

## Router
<details>
<summary>Setting up</summary>

- needed for adding navigation URLs
- `imports: [AppRoutingModule]` add module to `app.module.ts`
- `<router-outlet></router-outlet>` directive to the html, where we want to load the components from routes
```TypeScript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
// import all the components
// declarations: [] is not needed, all the components are declared in the app.module.ts

// add routes before the class
const appRoutes: Routes = [{...}];

@NgModule({
  imports: [RouterModule.forRoot(appRoutes)], // register routes (add configuration)
  // or hack for old browsers and servers with full paths (not returning index.html on 404 error)
  imports: [RouterModule.forRoot(appRoutes, { useHash: true })],
  exports: [RouterModule] // export what should be imported and accessible in another module
})
export class AppRoutingModule {}
```
```TypeScript
// app.module.ts
@NgModule({
  imports: [AppRoutingModule]
})
```

</details>

<details>
<summary>How to add a route?</summary>

```TypeScript
const appRoutes: Routes = [{
  path: '', // for starting (root) page
  path: 'users', // without `/` (error)
  path: ':id', // to use dynamic paths
  path: '**', // catches all paths, which are not specified, must be the last route
  component: ServerComponent, // which component should be displayed when the path will be reached
  redirectTo: 'path', // but without component
  pathMatch: 'full', // reconfigures the default 
  children: [{ route }], // array of routes, `<router-outlet>` required on parent component
  canActivate: [AuthGuard],
  canActivateChild: [AuthGuard],
  canDeactivate: [CanComponentDeactivate],
  canDeactivateChild: [CanComponentDeactivate],
  data: { message: 'Page not found!' }, // to pass some static data
  resolve: { server: ServerResolver } // to pass some dynamic data
}];
```

</details>

<details>
<summary>How to add a link for the navigation to the UI?</summary>

```HTML
<!-- routes can be absolute and relative (from current component) -->
<a href="/recipes">=== type manually, works, but reloads the app</a>
<!-- angular catches the event and prevents default -->
<a routerLink="/recipes">With no reload</a>
<!-- or -->
<!-- second (and more) path without `/` -->
<a [routerLink]="['/users', 'user']">With no reload</a>
```

</details>

<details>
<summary>Set to active, nav programmatically</summary>

- `routerLinkActive="class-name"` could be added to a link or it's wrapper
- `[routerLinkActiveOptions]="{ exact: true }"` for exact path match (full)

Navigating programmatically
- `constructor(private router: Router) { }` from `@ang/router` inject
- `this.router.navigate(['/users', 'user'])` like in `[routerLink]`, but doesn't know about current route
- `route: ActivatedRoute` from `@ang/router` inject, contains current route object
- `this.router.navigate([...], { relativeTo: this.route })`
- `this.router.navigate([...], { relativeTo: this.route, queryParamsHandling: '...' })`
  - `merge` merges current + navigate to params
  - `preserve` to keep only current params

</details>

<details>
<summary>How to get the parameters from the dynamic paths and render specific details?</summary>

```TypeScript
// app.module.ts
@NgModule({
  imports: [
    RouterModule.forRoot([
      { path: 'products/:id', component: ProductComponent }
    ])
  ]
})

// components/product/product.component.ts
import {Component, OnInit} from '@angular/core';
// specific to each component that the Angular Router loads
// contains information about the route and the route's parameters
import {ActivatedRoute} from '@angular/router';
import {products} from '../mocks/products';

@Component({/*...*/})
export class ProductComponent implements OnInit {
  product: Product;

  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    // static method, no re-instantiation of the component
    // to access the parameter in the initialization, not dynamic
    const routeParams = this.route.snapshot.paramMap;
    const productId = Number(routeParams.get('id'));
    // or
    const productId = Number(this.route.snapshot.params['id']);

    this.product = products.find(product => product.id === productId);
  }
}
```

- but by default Angular doesn't re-instantiate the component we currently in
- `this.route.params.subscribe((params: Params) => this.id = params['id])` for dynamical use the params observable
- don't need to unsubscribe, for this case Angular does it automatically on component is destroyed

</details>

<details>
<summary>Query parameters and fragments</summary>

Via links
- `[queryParams]="{ allowEdit: '1', id: '2' }"` to `?allowEdit=1&id=2` bindable property of router directive
- `[fragment]="'loading'"` to `#loading`

Programmatically
- `constructor(private router: Router)` from `@ang/router`
- `this.router.navigate(['/users', id, 'edit'], { queryParams: { allowEdit: '1' }, fragment: 'loading' })`
- `queryParamsHandling: 'preserve' / 'merge'` don't forget to add

Getting parameters and fragments
- `constructor(private route: ActivatedRoute)` from `@ang/router`
- `this.route.snapshot.queryParams / fragment` for static
- `this.route.queryParams / fragment.subscribe()` for dynamic

</details>

<details>
<summary>Guards: canActivate</summary>

- for guards it's enough to have a snapshot, because guards are always get executed (reloads)
- to protect the route, runs before entering the route
- `canActivate(Child): [AuthGuard]` add to the route to protect route + children or children only
- `auth-guard.service.ts` export `AuthGuard(Service)`
- `CanActivate(Child)` implements from `@ang/router`
- for ex add some fake service
  ```TypeScript
  export class AuthService {
    isLoggedIn = false;
    
    isAuthenticated() {
      return new Promise((resolve, reject) => {
        setTimeout(() => { resolve(this.isLoggedIn); }, 800);
      });
    }
    
    login() {
      // some logic
    }
  
    logout() {
      // some logic
    }
  }
  ```
- `AuthService` provide on the module level
- `@Injectable()` add to guard service, provide on the module level
- ```TypeScript
  constructor(private authService: AuthService, private router: Router) {}
  
  canActivate( // can run both async and static
    route: ActivatedRouteSnapshot, 
    state: RouterStateSnapshot // from @ang/router
  ): Observable<boolean> | Promise<boolean> | boolean { // from 'rxjs/Observable
    return this.authService.isAuthenticated()
      .then((authenticated: boolean) => {
        if (authenticated) { 
          return true; 
        } else {
          return false;
          // or
          this.router.navigate(['/']);
        }
      }
    }
  }
  ```

</details>

<details>
<summary>Guards: canDeactivate</summary>

- for example not to leave the page without saving the data in the form
- `canDeactivate(Child): [CanDeactivateGuard]` add to the route to protect route + children or children only
- `can-deactivate-guard.service.ts` export `CanDeactivateGuard(Service)`
- ```TypeScript
  export interface CanComponentDeactivate {
    canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
  }

  export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {
    canDeactivate(
      component: CanComponentDeactivate, 
      route: ActivatedRouteSnapshot, 
      state: RouterStateSnapshot, 
      nextState?: RouterStateSnapshot
    ): Observable<boolean> | Promise<boolean> | boolean {
      return component.canDeactivate();
    }
  }
  ```
- add logic to component
- ```TypeScript
  export class RecipeComponent implements CanComponentDeactivate {
    canDeactivate(): Observable<boolean> | Promise<boolean> | boolean {
      if (!this.allowEdit) {
        return true;
      }

      if (this.allowEdit && this.edited && !this.saved) {
        return 'Confirmation here resolved to boolean';
      } else {
        return true;
      }
    }
  }
  ```

</details>

<details>
<summary>Passing data to route</summary>

Plain data (static)
- `data: { message: 'Page not found!' }` add to the route
- access the data from component
- ```TypeScript
  constructor(private route: ActivatedRoute) { }

  doSomething() {
    this.route.snapshot.data['message']; // static
    this.route.data.subscribe((data: Data) => console.log(data['message'])); //dynamic
  }
  ```

Complex data (dynamic)
- need to use a resolver, which helps to run the code before the route is activated
- the resolver doesn't decide whether the component should or not be rendered, component always get rendered
- resolver does some preloading before the route activates (could also be done in `ngOnInit`, but that way the component initiated first and then the data fetches)
- `resolve: { server: ServerResolver }` add to the route
- `server-resolver.service.ts`
- provide the resolver on module level
- ```TypeScript
  export class ServerResolver(Service) implements Resolve<Server> { // from @angular/router
    resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Server> | Promise<Server> | Server {
      return this.serversService.getServer(+route.params['id']);
    }
  }
  ```
- `this.route.data.subscribe((data: Data) => this.server = data['server']);` access the data from the component

</details>

<details>
<summary>Learn more</summary>

- [Docs: In-app navigation: routing to views](https://angular.io/guide/router)

</details>

## Forms (Template Driven)
<details>
<summary>Basic idea</summary>

- view <= conception => logic
```HTML
<form>
  <input name="name" ...>
  <input name="email" ...>
</form>
```

```TypeScript
{
  value: {
    name: 'Max',
    email: 'test@test.com'
  },
  valid: true
}
```
- <b>template-driven</b> approach - angular infers the FormObject from the DOM
- <b>reactive</b> approach - form is created programmatically and synchronized with DOM

</details>

<details>
<summary>How to display and update properties with NgModel?</summary>

```TypeScript
// app.module.ts
import {NgModule} from '@angular/core';
import {FormsModule} from '@angular/forms';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule
  ]
})
export class AppModule {}
```
```HTML
<!-- app.component.ts -->
<label for="name">Name:</label>
<!-- this syntax can only set a data-bound property -->
<input id="name" type="text" [(ngModel)]="currentItem.name">
<!-- to customize your configuration - can write the expanded form, -->
<!-- which separates the property and event binding -->
<!-- use property binding to set the property -->
<!-- and event binding to respond to changes -->
<input 
  id="name-uppercase"
  type="text"
  [ngModel]="currentItem.name" 
  (ngModelChange)="setUppercaseName($event)"
>
```

</details>

<details>
<summary>For what HTML elements does NgModel directive work?</summary>

- for elements supported by `ControlValueAccessor` (Angular provides value accessors for all of the basic HTML form elements)
- to apply `[(ngModel)]` to a non-form native element or a third-party custom component, you have to write a value accessor
- writing a component, you don't need a value accessor or `NgModel` if you name the value and event properties according to the two-way binding syntax (`x` and `xChange`)

</details>

<details>
<summary>TD creation</summary>

- all the functionality is added to template
- `<form>` no `action="..."` or `method="..."` needed
- import `FormsModule` to the module
- angular automatically creates a form object for `<form>` in template, but doesn't detect the controls inside
- add `ngModel` to a control to register
- add html attr `name="..."`
- to submit add `(ngSubmit)="onSubmit()"` to a form
- to access the form use `<form (ngSubmit)="onSubmit(f)" #f>` local reference
- `onSubmit(form: HTMLFormElement) {}`
- to get the data object add `#f="ngForm"`
- `onSubmit(form: NgForm) {}` from `@ang/forms`
- could be also accessed via `@ViewChild('f') form: NgForm;`

</details>

<details>
<summary>TD Validation</summary>

- add to inputs angular directives
  - `required` works as directive and attribute
  - `email` directive
- angular adds both to form and control state classes like `ng-dirty`, `ng-touched`, `ng-valid`
- to enable native validation add `ngNativeValidate` to a control
- `[disabled]="!f.valid`
- `.ng-invalid.ng-touched` to not show error borders on the start (adds not valid class when first loads)
- `<input ... #email="ngModel">` like with ngForm on the form local reference and `<span *ngIf="!email.valid && email.touched">Error text</span>`

</details>

<details>
<summary>TD Preselected values</summary>

- `<input ... [ngModel]="valueString">` and `valueString = "some value";` in .ts file
- works because of prop binding, no need to use two-way binding
- if we need to show output on keydown, also can use a two-way binding `[{ngModel}]="property"`

</details>

<details>
<summary>TD Grouping controls</summary>

- can also validate a group
- to access from ts file add local reference to a group like in controls or form
```HTML
<div class="controls-wrapper" ngModelGroup="userData" #userData="ngModelGroup"></div>
```

</details>

<details>
<summary>TD Radio buttons</summary>

```TypeScript
public genders = ['male', 'female'];
```
```HTML
<div *ngFor="let gender of genders">
  <label>
    <!-- without preselected value -->
    <input type="radio" name="gender" ngModel [value]="gender">
    <!-- or with preselected value use property binding -->
    <input type="radio" name="gender" [ngModel]="..." [value]="gender">
    {{ gender }}
  </label>
</div>
```

</details>

<details>
<summary>TD Set and patch values</summary>

```TypeScript
@ViewChild('f') form: NgForm; // to access the form

// have to add all values, sets the whole form (via input name attribute)
this.form.setValue({
  userData: {
    username: suggestedName,
    email: ''
  },
  secret: 'pet',
  gender: 'male'
});

// accessible only on inner .form method in form container (NgForm)
// to patch only needed values (doesn't override other values)
this.form.form.patchValue({
  userData: {
    username: suggestedName
  }
});
```

</details>

<details>
<summary>TD Use form data</summary>

```TypeScript
this.form.value.userData.username; // group => input name attribute
this.form.value.questionAnswer; // input name attribute
```

</details>

<details>
<summary>TD Reset form</summary>

```TypeScript
// resets also specific classes (ng-pristine, ng-touched, ...)
// can pass value like in setValue to reset to some specific values
this.form.reset();
```

</details>

<details>
<summary>Learn more</summary>

- [Docs: Introduction to forms in Angular](https://angular.io/guide/forms-overview)

</details>

## Forms (Reactive)
<details>
<summary>How to create a form using FormBuilder?</summary>

```TypeScript
// app/components/simple/simple.component.ts
import {Component} from '@angular/core';
// import the service
import {FormBuilder} from '@angular/forms';

@Component({
  selector: 'app-simple',
  templateUrl: './simple.component.html',
  styleUrls: ['./simple.component.css']
})
export class NameComponent {
  // create the form
  loginForm = this.formBuilder.group({
    login: '',
    password: ''
  });
  // inject the service
  constructor(private formBuilder: FormBuilder) {}

  onSubmit(): void {
    console.log(this.loginForm.value);
    this.loginForm.reset();
  }
}
```
```HTML
<!-- bind the form group and submit event -->
<form [formGroup]="loginForm" (ngSubmit)="onSubmit()">
  <!-- bind fields to from controls using names -->
  <ul>
    <li>
      <label for="login">Login</label>
      <input formControlName="login" id="login" type="text">
    </li>
    <li>
      <label for="password">Password</label>
      <input formControlName="password" id="password" type="password">
    </li>
  </ul>
  <button type="submit">Login</button>
</form>
```

</details>

<details>
<summary>R Creation</summary>

- `ReactiveFormsModule` from `@angular/forms` add on module level
- `form: FormGroup` from `@angular/forms`
- can initiate form when declare a variable, but better in the method, for example in `ngOnInit` or other, but before the template is initiated

```TypeScript
this.form = new FormGroup({
  // use the quotes because connected to HTML, otherwise may be optimized by webpack
  'username': new FormControl(null), // presetValue, syncValidator(s), asyncValidator(s)
  'gender': new FormControl('female')
})
```

</details>

<details>
<summary>R Sync form and HTML</summary>

- by default `<form>` is only created, but not connected to the ts form
- use directives from the ReactiveFormsModule to connect
- `<form [formGroup]="form">` prop binding needed because we pass here our created form
- don't add name attribute or validation on controls (not needed)
- `formControlName="username"` here we pass a string, prop binding is also available

</details>

<details>
<summary>R Submit a form</summary>

- same as in TD, but without `#f`, because already have the form in ts `(ngSubmit)="onSubmit()"`
- all the object, passed on form creation we can get as a value of a form

</details>

<details>
<summary>R Access to controls</summary>

- there can be an error/bug with accessing controls in the template (can't use casting) due to the way TS works and Angular parses templates (doesn't understand TS there)
```TypeScript
// contains the control of type FormControl
// .valid .touched ... also available
this.form.get('username'); // control
this.form.get('userData.username'); // group => control
```

</details>

<details>
<summary>R Grouping controls</summary>

- `FormGroup` can be used inside the actual form (which is also a `FormGroup`)
- on a view wrap controls and add `formGroupName="userData"`
```TypeScript
this.form = new FormGroup({
  'userData': new FormGroup({
    'username': new FromControl(null),
    'email': new FormControl(null)
  })
});
```

</details>

<details>
<summary>R Arrays of controls</summary>

```HTML
<button (click)="onAddHobby()">Add hobby</button>
<ul formArrayName="hobbies">
  <!-- add controls, access control name by index in the array -->
  <li *ngFor="le hobbyControl of form.get('hobbies').controls; let i = index">
    <input type="text" [formControlName]="i">
  </li>
</ul>
```
```TypeScript
this.form = new FormGroup({
  'hobbies': new FormArray([...]) // could be empty
});

onAddHobby() {
  const control = new FormControl(null);
  // here TS needs casting for the array part
  (<FormArray>this.form.get('hobbies')).push(control);
}
```

</details>

<details>
<summary>R Validation</summary>

- don't add attributes to html (like required), add in ts to a control
- `username: new FormControl(null, Validators.required)` from `@angular/corms` don't execute here, pass only the reference, Angular will execute the method when the control changes
- for multiple validators `[Validators.required, Validators.email]`
- to check validation don't forget to check only touched controls `!form.get('username').valid && form.get('username').touched`

</details>

<details>
<summary>R Custom validators</summary>

- validator is just a function, which runs when Angular checks the validity of the control and when control is changed
```TypeScript
forbiddenUsernames = ['Anna', 'Jack'];

// if we use this class inside the validator function, don't forget to bind
// when Angular calls the method, this doesn't refer to our class
[Validators.required, this.forbiddenNames.bind(this)]

// [s: string] ts syntax for the key to be interpreted as a string
// error is added to control (not form) object 'errors'
forbiddenNames(control: FormControl): {[s: string]: boolean} {
  if (this.forbiddenUsernames.indexOf(control.value) !== -1) {
    return {
      'nameIsForbidden': true
    }
  }

  // if validation is successful, return null or nothing
  return null;
}
```

</details>

<details>
<summary>R Error codes</summary>

```TypeScript
// to check if our custom error exists
form.get('userData.username').errors['nameIsForbidden'];

// for built-in validators
form.get.('...').errors['required'];
```

</details>

<details>
<summary>R Custom async validators</summary>

- for example to check if the email or username are already exist in the database
- like with normal validators, single or array
- don't forget to bind class if using `this`
```TypeScript
'email': new FormControl(null, Validators.required, this.forbiddenEmails)

forbiddenEmails(control: FormControl): Promise<any> | Observable<any> {
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      if (control.value === 'test@test.com') {
        resolve({'isEmailForbidden': true});
      } else {
        resolve(null);
      }
    }, 1500);
  });

  return promise;
}

```

</details>

<details>
<summary>R Reacting to status and value changes</summary>

- available on both from and control
```TypeScript
this.form.valueChanges.subscribe((value) => console.log(value));
this.form.statusChanges.subscribe((status) => console.log(status)); // VALID PENDING
```

</details>

<details>
<summary>R Set and patch values and reset a form</summary>

```TypeScript
// to set values to the whole form use
this.form.setValue({...});

// to patch only some values use
this.form.patchValue({...});

// to reset the form use
this.form.reset(); // can also pass {} with values to reset to
```

</details>

<details>
<summary>Learn more</summary>

- [Docs: Introduction to forms in Angular](https://angular.io/guide/forms-overview)

</details>

## 12 - Modules
<details>
<summary>General info</summary>

- bundles different pieces into one package (components, directives, services, pipes, etc)
- have to group because Angular doesn't scan the files, have to inform what will be used
- requires at least 1 module (AppModule) but may be split into multiple modules
- Angular analyzes NgModules to understand your app and its features
- define all the building blocks your app uses: Components, Directives, Services, etc.
- core Angular features are wrapped in Angular modules (ex. FormsModule) to load them only when needed
- custom modules mostly for big projects
- gives Angular info on which features to use
- can't use a feature / building block without including it in a module

</details>

<details>
<summary>Analyzing the AppModule</summary>

- the service could be used not only in the module it's provided in
- bootstrap typically includes only one root component but if there are more components, will create a different root, will be detached from other components 
- every module in Angular works on its own, they don't communicate with each other, we can use the declared components only in the module
- have to export to be available where the module is imported
```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';

@NgModule({
  // components, directives, pipes
  declarations: [],
  // modules
  imports: [],
  // for exported features to use in other modules
  exports: [],
  // root needed on start component
  bootstrap: [],
  // services, interceptors
  providers: [],
  // for the case when we want to create a dynamic component in code
  entryComponents: []
})
export class AppModule {}
```

</details>

<details>
<summary>Feature modules</summary>

- groups together the pieces, which are used in the certain area of the app (recipes, shopping-list, auth)
- leaner code, easy to work, needed for future optimization (lazy loading)
```TypeScript
// recipes.module.ts
@NgModule({
  // remove from AppModule
  declarations: [RecipesComponent, ...],
  exports: [RecipesComponent, ...]
})
export class RecipesModule {}
```
- `imports: [RecipesModule]` to the app module
- error: router-outlet is not a known element => using but this directive is provided by Angular, available from RouterModule
- RouterModule is used not only to config the routes, but also provides all the directives to use (like router-outlet)
- it's available in AppModule, but not in the RecipesModule (the modules live on their own, have to import!)
- only services could be set up once in the app module and used in different modules
1. `imports: [RouterModule]` for using router
2. `imports: [CommonModule]` not `BrowserModule` - special case (only one) as `BrowserModule` is used only once in the AppModule, does more than `ngIf` and `ngFor`, also some app startup work that only needs to run once
3. `imports: [ReactiveFormsModule]` to use forms

</details>

<details>
<summary>Adding routes to Feature modules</summary>

- `imports: [RouterModule.forChild(routes)]` will automatically merge these routes with root routes (.forRoot)
```TypeScript
// recipes-routing.module.ts
const routes: Routes = [{
  path: 'recipes', ... // + all the child routes, remove from app-routing
}];
@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class RecipesRoutingModule {}
```
- import to RecipesModule
- now routes are part of the general routing config (since we import the RecipesModule to AppModule)
- need not only add Components to router but have to declare them on the module level or there will be an error
- but now we load the components via router, no need to export them in the RecipesModule, Angular knows how to load components because of router

</details>

<details>
<summary>Shared modules</summary>

- to avoid code duplication we can outsource the shared features into the shared module and import where needed
- can have multiple shared modules
```TypeScript
// shared.module.ts
@NgModule({
  declarations: [AlertComponent, PlaceholderDirective, ...],
  imports: [CommonModule],
  exports: [AlertComponent, PlaceholderDirective, CommonModule, ...],
  entryComponents: [AlertComponent]
})
export class SharedModule {}
```
- here we just centralize the functionality, so need to export all the features to use in other modules
- can only declare directives once!
- can import modules several times in different modules
- imports are ok, but declarations are not => get an error
- the solution: to export from module and to import module to use it in the other module

</details>

<details>
<summary>Core modules</summary>

- to make the app module leaner
- can use the core module to move the services from AppModule => CoreModule (but `{providedIn: 'root'}` is better)
- for interceptors still good to use CoreModule
```TypeScript
// core.module.ts
@NgModule({
  providers: [
    // if not in 'root'
    RecipesService,
    ...,
    {
      provide: HTTP_INTERCEPTOR,
      ...
    }
  ]
})
export class CoreModule {}
```
- don't need to export services (automatically injected on the root level)
- but still need to import the CoreModule in the AppModule

</details>

<details>
<summary>Learn more</summary>

- [NgModules](https://angular.io/guide/ngmodules)
- [NgModule FAQ](https://angular.io/guide/ngmodule-faq)

</details>

## Observables
<details>
<summary>What is an observable, an observer and how does it handle the data?</summary>

- <b>Observable</b> - something we observe like publisher (also known as subject), data source, most common:
  - user events
  - http requests
  - triggered in code
- <b>Observer</b> - our code, our subscription
- Handling data:
  - Data
  - Errors
  - Completion (not always complete)
- added from `'rxjs'` package, not a part of TypeScript or Angular
- no need to import if we use Angular Observables
- need to import only when we use other Observables

</details>

<details>
<summary>Why do we need observables?</summary>

- let you pass messages between parts of your application
- recommended for event handling, asynchronous programming, and handling multiple values
- can deliver single or multiple values of any type, either synchronously (as a function delivers a value to its caller) or asynchronously on a schedule

</details>

<details>
<summary>Interval example</summary>

```TypeScript
import {OnInit, OnDestroy} from '@angular/core';
import {Interval, Subscription} from 'rxjs';

@Component({...})
export class NameComponent implements OnInit, OnDestroy {
  // some code here
  private intSubscription: Subscription;

  ngOnInit() {
    interval(1000).subscribe(count => console.log(count));

    // to be able to unsubscribe => prevents memory leaks
    this.intSubscription = interval(1000).subscribe(count => console.log(count));
  }

  ngOnDestroy() {
    this.intSubscription.unsubscribe();
  }
}
```

</details>

<details>
<summary>Custom</summary>

```TypeScript
// from 'rxjs', create - a function, rxjs passes
const customIntObservable = Observable.create(observer => { // rxjs passes the arg observer (listener) 
  let count = 0;
  
  setInterval(() => {
    observer.next(count); // next emits new value

    // when error, there is no complete, complete != error
    if (count > 3) {
      observer.error(new Error('Error message')); // error = observable is done, no need to unsubscribe
    }

    if (count === 5) {
      observer.complete(); // done, no args, just stops, unsubscribe not needed
    }

    count++;
  }, 1000);
});

this.ownIntSubscription = customIntObservable.subscribe(
  data => console.log(data), // 1 - data handler
  error => console.log(error), // 2 - error handler
  () => console.log('Complete!') // 3 - complete handler
);

ngOnDestroy() {
  this.ownIntSubscription.unsubscribe();
}
```

</details>

<details>
<summary>Operators</summary>

- to transform data before subscribing
- can transform in subscription, but operators are better and cleaner
- import operators from `'rxjs/operators'`
- there are a lot of different operators
- `tap` allows to execute code without altering the result
- `switchMap` allows to create a new observable by taking another observable's data (switches the observable to another one)
- `filter`
- `map`
- `catchError`
- `throwError`
- `take`
- `exhaustMap`
- `of` creates a new observable
- `withLatestFrom` allows to merge another observable into this observable
- ```TypeScript
  this.ownIntSubscription = this.customIntObservable.pipe(
    filter(data => data > 0),
    map((data: number) => 'Round: ' + (data + 1))
  ).subscribe();
  ```

</details>

<details>
<summary>Subject</summary>

- using instead of `EventEmitter` for cross-component communication through service: better, more efficient, operators available
- `activatedEmitter = new Subject<boolean>();` add to service from 'rxjs'
- `this.userService.activatedEmitter.next(true);` from the 1st component
- `this.userService.activatedEmitter.subscribe();` form the 2nd component
- don't forget to unsubscribe
- in Observable we call `.next()` only from the inside, but in Subject can be called from the outside
- perfect for cross-component communication (triggered by app when no server involved)
- `@Output()` still uses `EventEmitter`, Subject here is not suitable

</details>

## Http Client
<details>
<summary>Http and backend interaction</summary>

- Angular => [http request] server => [REST/GraphQL etc] database
- database => server => [http response] Angular
- HTTP verb (action) `POST, GET, PUT, PATCH ...`
- URL (API endpoint) `/post/1`
- Headers (metadata) `{'Content-type': 'application/json'}`
- Body (optional) `{title: 'New Post'}`

</details>

<details>
<summary>How to use HttpClient in a service?</summary>

- it's better to use service for http requests handling 
- let the component be simple, divide data management from view
- works with a stream of data from the server
```TypeScript
// app.module.ts
import {NgModule} from '@angular/core';
// registers the providers to use the HttpClient service
import {HttpClientModule} from '@angular/common/http';

@NgModule({
  imports: [HttpClientModule]
})
export class AppModule {}

// simple.service.ts
import {Injectable} from '@angular/core';
// import HttpClient service
import {HttpClient} from '@angular/common/http';

@Injectable({providedIn: 'root'})
export class SimpleService {
  items = [];

  constructor(private http: HttpClient) {}

  getItems() {
    // sends an HTTP request, and returns an observable
    // that emits the requested data for the response
    return this.http.get('./mocks/data/items.json');
  }
}

// components/basic.component.ts
import {Component} from '@angular/core';
import {SimpleService} from '../simple.service.ts';

@Component({})
export class BasicComponent {
  items = this.simpleService.getItems();

  constructor(private simpleService: SimpleService) {}
} 
```
```HTML
<!-- use async pipe to get the data -->
<ul>
  <li *ngFor="let item of items | async">
    {{ item.name }}
  </li>
</ul>
```
- if the components are not interested in receiving data, can subscribe in service
- if data needed in the component, `return get/post` and don't subscribe
- or use `Subject` and `.next` method
- where using loader and fetching, don't forget to reset `isLoading` to `true` first!


</details>

<details>
<summary>Sending a POST request</summary>

- `import { HttpClientModule } from '@angular/common/http';` to `imports: [..., HttpClientModule]` on module level
- inject http client on component level
- if using firebase, add `.json` to the URL (firebase requirement)
- `.post` method returns an observable, no need to unsubscribe (it'll complete in the end, also it's Angular feature)
- browsers first send `OPTIONS` request to check if `POST` is available
- if 200 => send actual `POST` request
```TypeScript
export class NameComponent {
  constructor(private http: HttpClientModule) {}

  // sending post to server
  onCreatePost(postData: {title: string}) {
    // if we don't subscribe to an observable, Angular won't send the request
    // because of optimization, not interested in response? why send?
    this.http.post('<url>', postData).subscribe(responseData => console.log(responseData));
  }
}
```

</details>

<details>
<summary>Getting data</summary>

- add a method to fetch posts, use it in `ngOnInit`, whenever you want to update posts
```TypeScript
private fetchPosts() {
  // same as with the POST, need to subscribe or won't be sent
  this.http.get('<url>').subscribe(posts => console.log(posts));
}
```

</details>

<details>
<summary>Transforming data using operators</summary>

- can transform inside subscribe method, but operators are better (cleaner code)
- outputting the data is simple, don't forget to add ui if there is no posts
```TypeScript
// post.model.ts
export interface Post {
  title: string;
  content: string;
  id?: string;
}

// adding types to our requests (all requests are generics, so we can add type to <...>)
// also possible in operator, but better on the request
.post<{name: string}>(...);

.get<{[key: string]: Post}>(...) // response body type
.pipe(map(responseData => {
  const posts = [];
  
  for (const key in responseData) {
    // good to check in 'for ... in' loop if we're not trying to access some prototype method
    if (responseData.hasOwnProperty(key)) {
      // use spread to copy an object to add some data
      // in firebase key is unique encrypted name, good for id and access later to update or delete posts
      posts.push({...responseData[key], id: key});
    }
  }

  return posts;
}))
.subscribe(posts => console.log(posts));
```
```TypeScript
public isFetching = false;

// can also add a loader
// don't forget to add !isFetching to no posts and posts display views
public fetchPosts() {
  this.isFetching = true;
  this.http.get(...).subscribe(() => this.isFetching = false);
}
```

</details>

<details>
<summary>Sending a delete request</summary>

- not always allowed by backend API
- add delete method to the service
```TypeScript
deletePosts() {
  return this.http.delete('url');
}
```
- get the data (subscribe to null the array) from component
```TypeScript
onClearPosts() {
  this.postsService.deletePosts().subscribe(() => this.posts = []);
}
```

</details>

<details>
<summary>Handling errors</summary>

- firebase settings to rules (simulate error to test)
- add a reaction to an error (different ways)
- pass 2nd argument to subscribe method, which handles error
```TypeScript
(error) => this.error = error.message;
```
- subject for using error handling (especially for cases when we do not subscribe in the components)
- add to service
```TypeScript
error = new Subject<string>(); // from rxjs
...
(error) => this.error.next(error.message);
```
- and subscribe in the component
```TypeScript
this.errorSub = this.postsService.error.subscribe((errorMsg) => {
  this.error = errorMsg; 
});

ngOnDestroy() {
  this.errorSub.unsubscribe();
}
```

</details>

<details>
<summary>Cases when error can occur in different situations</summary>

- there is also an operator to assist with errors, for example when we pipe data (not always http related)
- `throwError` from `rxjs/operators` is specific for this case also possible, wraps error into observable
```TypeScript
{ return throwError(errorResult); } // inside catchError
```
```TypeScript
// from 'rxjs/operators'
// need to pass something, which could be subscribed to (need to subscribe)
// subject if possible
.pipe(map(...), catchError(errorResponse => {
  // do something with the error (analytics or UI)
}));
```

</details>

<details>
<summary>Good practice for UI handling errors</summary>

- add a button to remove an error from the UI
- don't forget to reset isLoading and other props for correct messages on the view

</details>

<details>
<summary>Setting headers</summary>

- for auth (ex), some custom headers etc. (depends on server API)
- any http method has the last argument (post - 3rd) (get - 2nd), which is an object with some configurations
```TypeScript
// from '@angular/common/http
{ headers: new HttpHeaders ({
  'Custom header': 'Hello'
}) }
```

</details>

<details>
<summary>Setting query parameters</summary>

- also depends on what parameters are supported by server API
- add to the same object as for headers
```TypeScript
{
  params: new HttpParams().set('print', 'pretty')
}
```
- works the same as if you add `?print=pretty` to the URL, but params is more clear and better
- for more params
```TypeScript
let params = new HttpParams();
// append returns a new object
params = params.append('print', 'pretty');
params = params.append('custom', 'value');
{
  params: params
}
```

</details>

<details>
<summary>Observing different types of responses</summary>

- for the cases when we need not / not only body, but other props of response data (headers, status, etc)
- added to the same config object as query params or headers
```TypeScript
{
  observe: 'body' // default
  observe: 'response' // whole response
  observe: 'events' // a series of events encoded with numbers
  // like 4 = response
}
.pipe(tap(event => console.log(event)));
if (event.type === HttpEventType.response) {...}
```
- for ex needed to give info to the user if something is being sent etc

</details>

<details>
<summary>Changing the response body type</summary>

- also added to the same config object as headers etc
```TypeScript
{
  responseType: 'json' // default
  responseType: 'text'
  responseType: 'blob'
  ...
}
```

</details>

<details>
<summary>Learn more</summary>

- [Docs: Communicating with backend services using HTTP](https://angular.io/guide/http)

</details>

## 15 - Interceptors
<details>
<summary>General info</summary>

- when to use? for ex when we want to attach the same custom header to all our requests, more realistic when we need to auth user and send a header
- `auth-interceptor.service.ts` export `AuthInterceptorService`
- `implements HttpInterceptor` from `@angular/common/http`
```TypeScript
// next - function, which will forward the request
intercept(req: HttpRequest<any>, next) {...}
```
- interceptor runs a code before the request lives our app, we need to add next to allow the request continue its journey, otherwise error
```TypeScript
{
  console.log('Request is on its way');
  return next.handle(req);
}
```
- provide in app module in a special way
```TypeScript
providers: [{
  // from '@angular/common/http
  // a token how ang identifies that should be treated
  // as an http interceptor and run in the whole app
  provide: HTTP_INTERCEPTORS,
  useClass: AuthInterceptorService,
  // if > 1 interceptors
  multi: true
}]
```
- angular by default will run the interceptor with all the http methods, but we can configure the restriction inside the interceptor function
```TypeScript
intercept(...) {
  if (req.url === '...') {
    // do something
  }
}
```
- inside we can modify the request object (case with added headers), but req object itself is immutable
```TypeScript
const modifiedReq = req.clone({
  url: '...',
  headers: req.headers.append('Auth', 'some-value')
});
return next.handle(modifiedReq);
```

</details>

<details>
<summary>Response interceptors</summary>

- add something to `return next...` of the intercept function
```TypeScript
return next.handle(modifiedReq)
  // here in the interceptor we always get the events,
  // no matter what was chosen on the request http method
  .pipe(tap((event) => {
    if (event.type === HttpEventType.response) {
      console.log(event.body);
    }
  }));
```
- be careful not to change data to break the application

</details>

<details>
<summary>Multiple interceptors</summary>

- the order in the app module matters, the first will be executed first
```TypeScript
providers: [{
  provide: HTTP_INTERCEPTORS,
  useClass: AuthInterceptorService,
  multi: true
}, {
  provide: HTTP_INTERCEPTORS,
  useClass: LoggingInterceptorService,
  multi: true
}]
```

</details>

## 16 - Authentication
<details>
<summary>General info</summary>

<img width="500" src="./images/auth.jpg" alt="authentication process">

- user enters data on client
  - can't check on client
  - insecure
- send auth data to server to authenticate the user
- server validates user
  - if valid - sends a token to client (json web-token typically)
  - encoded (not encrypted) - string with lots of metadata
  - could be unpacked and read by a client
  - generated on the server with secret algorithm only server knows, so only the server can validate the incoming token for validity
- client stores token in browser localStorage
- when one more time client sends to a server a request, it attaches the stored token in header or query param
- can't generate, edit or change the token on the client (not secure!)

- traditionally (not SPA) we work with session (stored on server, state existed), in stateless server and client don't know about each other

</details>

<details>
<summary>Adding a sign up request</summary>

- `auth.service.ts` `AuthService`
- `@Injectable()` from `@angular/core`
- `constructor(private http: HttpClient) {}` inject http service from `@angular/http`
- add the interface of response data (good practice)
- add method to a class
```TypeScript
signup(email, password) {
  return this.http.post<AuthResponseData>('url', {
    email,
    password
  });
}
```

</details>

<details>
<summary>Sending the sign up request</summary>

- in the form containing the component
```TypeScript
onSubmit() {
  if (!form.valid) {
    return;
  }

  const {email, password} = form.value;

  this.authService.signup(email, password)
    .subscribe(data => console.log(data), error => {});

  form.reset();
}
```
- inject the service `constructor(private authService: AuthService) {}`
- don't forget to add `isLoggedIn` logic

</details>

<details>
<summary>Adding loading spinner</summary>

- add prop on top `isLoading = false;`
- on submit before sending the request set to true
- and back to false on success or errors

</details>

<details>
<summary>Adding an error handling</summary>

- add prop on top `error: string = null;`
- set an error message in error handler of the http request
- for custom error handling better to use in service with operator `catchError/throwError` (because have to wrap an observable to pass to the subscribe)
- in service add after the request
```TypeScript
.pipe(catchError(errorRes => {
  let errorMessage = 'Some default error message';

  if (!errorRes.error || !errorRes.error.error) {
    return throwError(errorMessage);
  }

  switch(errorRes.error.error) {
    case 'EMAIL_EXISTS':
      errorMessage = 'Email exists';
      break;
  }

  return throwError(errorMessage);
}))
```

</details>

<details>
<summary>Login handling</summary>

- also when 2 similar subscriptions handling
```TypeScript
onSubmit() {
  // ...
  let authObservable: Observable<AuthResponseData>;

  if (this.isLoginMode) {
    authObservable = this.authService.login(email, password);
  } else {
    authObservable = this.authService.signup(email, password);
  }

  authObservable.subscribe();
}
```

</details>

<details>
<summary>Handling errors in separate method</summary>

- remove code from `.pipe(catchError(...))` to other method
```TypeScript
// from @angular/http
private handleError(errorRes: HttpErrorResponse) {}
```
- use where we need to catch an error `catchError(this.handleError)`

</details>

<details>
<summary>Creating and storing user data</summary>

- create a user model (with user data and validation if token exists and not expired)
```TypeScript
export class User {
  constructor(
    public email: string,
    public id: string,
    private _token: string,
    private _tokenExpirationDate: Date
  ) {}
}

get token () {
  if (!this._tokenExpirationDate 
    || new Date() > this._tokenExpirationDate) {
      return null;
    }

    return this._token;
}
```
- add a user subject in the auth service `user = new Subject<User>();`
- emit a new user every time the user changes (login / logout / exp date / etc.)
- add tap operator after catchError for handling user data
```TypeScript
private handleAuthentication(email: string, id: string, token: string, expIn: number) {
  const expDate = new Date(new Date.getTime() + expIn * 1000);
  const user = new User(email, id, token, expDate);

  this.user.next(user);
}

tap(this.handleAuthentication());
```

</details>

<details>
<summary>Reflecting the Auth status in the UI</summary>

- add user navigation on success of login (not in the service is better if you don't want to mix UI and service)
```TypeScript
// AuthComponent
// from @angular/router
constructor(private router: Router) {}

resData => {
  // ...
  this.router.navigate(...);
}
```
- change controls in the header (and other dependable UI), add logout button (later based on token, for now on user)
```TypeScript
// HeaderComponent
constructor(private authService: AuthService) {}

ngOnInit() {
  this.userSub = this.authService.user.subscribe(
    user => this.isAuth = !!user
  );
}

ngOnDestroy() {
  this.useSub.unsubscribe();
}
```
- update the logic on the UI with `*ngIf`

</details>

<details>
<summary>Adding the token to outgoing requests</summary>

- In the data-storage.service.ts
```TypeScript
// DataStorageService
constructor(private authService: AuthService) {}
```
- Update auth service to be able to fetch data about user on demand
  - can store token in a variable, but there is a better way
  - use `BehaviorSubject` almost = `Subject` but gives the subscribers immediate access to the previously emitted value even if they haven't subscribed at the point of time when the value was emitted. That means we can get access to the currently active user even if we only subscribe after that user has been emitted, so when we fetch data and we only need the token at this point even if the user logged in before that time, we get the access to this latest user, therefore `BehaviorSubject` needs to be initialized with the starting value.
- Add to the data storage service where we fetch recipes. Operator `take()` gives the value `(1)` time and automatically unsubscribes. Because we need the user only when we fetch recipes, but not constantly.
```TypeScript
this.authService.user.pipe(take(1)).subscribe();
```
- Pipe user observable and http observable into one bigger observable. `exhaustMap()` waits for the 1st observable (user) to complete after we `take(1)` user, `exhaustMap(user => this.http...)` observable will replace out user observable in the higher observable chain
```TypeScript
....user.pipe(take(1), exhaustMap(user => this.http...), map(recipes => {}));
```
- Add the token either as a query string (param) or in the second argument of the `http` method
```TypeScript
'....json?auth=' + user.token
{
  // from @angular/common/http
  params: new HttpParams().set('auth', user.token)
}
```
- if the token is not valid => error but we add logout when token is expired

</details>

<details>
<summary>Attaching the token with an interceptor</summary>

- don't add `{providedIn: 'root'}`, interceptors provided differently
```TypeScript
// auth-interceptor.service.ts
// AuthInterceptorService
// @angular/common/http
implements HttpInterceptor
intercept(req: HttpRequest<any>, next: HttpHandler) {
  return next.handle(req);
}
```
- inject `AuthService` to get user and `this.authService.user.subscribe();`
- use `exhaustMap()` to return a request observable
```TypeScript
const modReq = req.clone({params: ...});
exhaustMap(user => next.handle(modReq));
```
- now interceptor will add token to all outgoing requests
- provide in module `HTTP_INTERCEPTORS`
- can specify either url or `if (!user) { return next.handle(req); }`
- fails on login because we have no user yet (= null in `BehaviorSubject`)

</details>

<details>
<summary>Adding logout</summary>

```TypeScript
// auth.service.ts
logout() {
  this.user.next(null);
  this.router.navigate(['/auth']);
}
```
- add `onLogout()`to where needed (ex. click on logout button in header)
- redirect in service because we have only 1 place to login but multiple to logout

</details>

<details>
<summary>Adding auto-login</summary>

- to keep the logged in state on reload
- store user either in `localStorage` or use cookie
- in `handleAuth` inside `AuthService` add save to local storage
```TypeScript
localStorage.setItem('userData', JSON.stringify(user));
```
- add autoLogin method
```TypeScript
autoLogin() {
  const userData = JSON.parse(localStorage.getItem('userData'));

  if (!userData) {
    return;
  }

  const loadedUser = new User(userData.email, ...);

  if (loadedUser.token) {
    this.user.next(loadedUser);
  }
}
```
- convert date string into Date (in JSON it's a string)
- use the method inside app component (first entry basically)

</details>

<details>
<summary>Adding auto logout</summary>

- need to clear user on token expired
- in auth service in logout clear the `localStorage.removeItem('userData');`
- set a timer for auto logout
```TypeScript
autoLogout(expirationDuration: number) {
  this.logoutTimer = setTimeout(() => {
    this.logout();
  }, expirationDuration);
}
```
- clear the timer in logout (in case it still exists)
```TypeScript
logout() {
  // ...
  if (this.logoutTimer) {
    clearTimeout(this.logoutTimer);
  }
  this.logoutTimer = null;
}
```
- call autologout every time we emit new user

</details>

<details>
<summary>Adding AuthGuard</summary>

- to prevent visiting for unauthorized users
- add `auth.guard.ts`
```TypeScript
// AuthGuard
implements CanActivate {
  canActivate(route: ActivatedRouteSnapshot, router: RouterStateSnapshot):
    boolean |
    Promise<boolean> |
    Observable<boolean> {
    return this.authService.user.pipe(map(user => !!user));
  }
}
```
- but we want to navigate
  - earlier with `tap` operator
  - now with `urlTree`
```TypeScript
<boolean | urlTree>
map(user => {
  const isAuth = !!user;

  if (isAuth) {
    return true;
  }

  return this.router.createUrlTree(['/auth']);
});
```
- don't set constant subscription, add `take(1)` before map

</details>

<details>
<summary>Useful links</summary>

- [Firebase Auth REST API](https://firebase.google.com/docs/reference/rest/auth)
- [JSON Web Tokens](https://jwt.io/)

</details>

## 17 - Lazy loading
<details>
<summary>General info</summary>

- separating the code into modules makes it easier to work with, but doesn't improve the performance
- by default (without lazy loading) all the modules are loaded from the start (for all routes: `/`, `/admin`, `/user`, `/recipes`, ...) even when we don't navigate there
- so we want to load like that:
```
'path' => FeatureModule
'/' => AppModule / CoreModule
'/admin' => AdminModule
'/user' => UserModule
'/recipes' => RecipesModule
...
```

</details>

<details>
<summary>Implementing lazy loading</summary>

- check files sizes in the network panel of the dev tools
- have to register the routes for the module (feature module needs to bring its own routes for lazy loading with `.forChild()`)
- have to change `path: ''` to the empty path
- add path to app-routing module for lazy loading to work
```TypeScript
// app-routing.module.ts
{
  path: 'recipes',
  // old syntax
  // recipes, not recipes-routing
  // angular doesn't know the class name, have to set
  loadChildren: './recipes/recipes.module#RecipesModule'
  // new syntax (old could not work in the new versions)
  loadChildren: () => import('./recipes/recipes.module').then(module => module.RecipesModule)
}
```
- `loadChildren` gives Angular the direction to only load the module when the user visits this path
- now the code is split and all the declarations will be put into separate code bundle, which will be downloaded on demand
- don't import in the top (even unused) files into the AppModule or will be loaded when the app starts
- also remove the module from `imports: []` => error (2 times imported)
- when we go to '/recipes', the RecipesModule will be loaded and we already will be on '/recipes', that's why change path to `''`

</details>

<details>
<summary>Preloading lazy loaded code</summary>

- to avoid delay can preload modules
```TypeScript
// app-routing.module.ts
.forRoot(routes, {preloadingStrategy: PreloadAllModules});
```
- default is `NoPreloading`
- `PreloadAllModules` - code is split, will be preloaded as soon as possible
- initial bundle is still small
- can build own preload strategies

</details>

## 18 - Ahead-of-Time Compilation

<details>
<summary>Ahead-of-Time vs Just-in-Time Compilation</summary>

1. Your code and templates include syntax only Angular understands (*ngFor etc)
2. TypeScript compiler compiles the code to JavaScript
3. Angular compiler (automatically included in the built code) compiles template syntax to JavaScript DOM instructions
4. JiT vs AoT
  - JiT - Angular template compiler runs in browser (at runtime)
    - the compiler is too large and affects the performance
    - nice to use for development
    - `ng serve` uses JiT compiler
  - AoT - Angular template compiler runs during build process (before the app is deployed)
    - here the compiler runs only before the app is deployed and not in the browser
    - AoT removes the compiler from the final bundle
    - good for production
    - `ng build --prod`

</details>

## 19 - NgRx
<details>
<summary>Application State</summary>

<img src="./images/app-state.png" alt="Application State">

- data that is imported into the application and displayed on the screen
- any information, which controls what should be visible is a state
- not only the data display, but also states like loading
  - initial ingredients
  - loading on auth component (not application state but local state)
- lost when the application refreshes
- persistent state is on backend

</details>

<details>
<summary>Application State management for small projects</summary>

- the application state could be managed with services, components, rxjs (recipes service manages recipes, stores the data on the server in a persistent state for not to be lost)

</details>

<details>
<summary>App State management for middle projects</summary>

<img src="./images/app-state-1.png" alt="Application State">

- rxjs (event in the UI => (State changing event => Observable => Operators => Listener) => Update UI) 

<img src="./images/rxjs.png" alt="RxJS">

- but has some issues
  - state can be updated anywhere
  - state is (possibly) mutable
  - handling side effects (like http management) is unclear (write in the component? or use in the service? etc)
  - no specific pattern is enforced

<img src="./images/rxjs-issues.png" alt="RxJS issues">

</details>

<details>
<summary>App State management for large projects</summary>

<img src="./images/redux.png" alt="Redux">

- Redux - the state management pattern and library that helps to implement this pattern
1. Has one central store (holds the app state - large object, that contains all the data the parts of your app need, single source of truth, that manages the entire app state).
2. Services and Components can still communicate with each other but they receive their state from the store
3. Sometimes we need to change the state (ex: add, delete, change the recipe)
4. Dispatch Actions (JS object with identifier (kind of action) and optionally the payload (if the action needs some data to complete (recipe add => attach the recipe to the action))) - supported by Redux
5. The action doesn't directly go to the store => it reaches the reducer
6. Reducer is just a JS function, that gets the state and the action (passed by Redux if used).
7. Reducer looks for an action identifier (add, delete the recipe) and performs the code on the state to update in immutable way
8. The reducer returns the new state, which is forwarded to the app store (overrides the old state of the app).
- With that approach we have a clear data flow
- In Redux it is unclear when and where you should send the http requests, async code was always a problem because reducers can only execute the sync code, so you can't send the http request from the reducer function

</details>

<details>
<summary>Differences between Redux and NgRx</summary>

<img src="./images/ngrx.png" alt="NgRx">

With Angular Redux could be used but NgRx is an Angular implementation of Redux.
- comes with injectable services, can access the store in any part of the app by injecting it
- uses rxjs and Observables - all the state is managed as one large Observable, many advantages (can use operators) to fetch the state in the component when needed in the way we need it, will not change the store
- uses TypeScript
- extra plus - managing side effects (http operations) - gives a tool to work with side effects easier

</details>

<details>
<summary>Adding NgRx to the project</summary>

- install the package `npm install --save @ngrx/store
- first add the reducer

</details>

<details>
<summary>Reducers</summary>

- it's just an ordinary function
- NgRx calls the functions and pass as arguments state and action
- we can setup an initial state (has to be a JS object)
```TypeScript

// to use as the type and change only here export the state interface
// import * as fromShoppingList from ''; naming convention for imports
export interface State {
  ingredients: Ingredient[];
  editedIngredient: Ingredient;
  editedIngredientIndex: number;
}

const initialState: State = {
  ingredients: [...],
  editedIngredient: null,
  editedIngredientIndex: -1
};

export function shoppingListReducer(state = initialState, action) {
  switch (action.type) {
    case 'ADD_INGREDIENT':
      return {
        ...state,
        // the ingredient should be a part of an action. change later
        ingredients: [...state.ingredients, action]
      };
    default:
      // to set the initial state use default and return unchanged state
      // very important to use the default state
      // on init store module sends one initial action to all reducers
      // also when the action is dispatch, it is sent to all reducers
      return state;
  }
}
```

</details>

<details>
<summary>Actions setup</summary>

- the naming convention is uppercase snake notation
- return state, which has to be immutable (copy the state and override the changed properties)
```TypeScript
// shopping-list/store/shopping-list.reducer.ts
import { Action } from '@ngrx/store';

// ...

export function shoppingListReducer(state, action: Action) {
  switch (action.type) {
    case 'ADD_INGREDIENT':
      return {
        ...state,
        // the ingredient should be a part of an action. change later
        ingredients: [...state.ingredients, action]
      };
  }
}
```
- have to standardize the action creation process to avoid mistakes (when using a string for type)
```TypeScript
// shopping-list/store/shopping-list.action.ts
import { Action } from '@ngrx/store';

export const ADD_INGREDIENT = 'ADD_INGREDIENT';
export const ADD_INGREDIENTS = 'ADD_INGREDIENTS';
// all the actions have to have a unique value through the whole app
// as they are sent to all reducers on dispatch
export const ADD_INGREDIENT = '[Shopping List] Add Ingredient';

export class AddIngredient implements Action {
  readonly type = ADD_INGREDIENT;
  // could be any (or no prop) name here, only type is needed
  payload: Ingredient;
}

export class AddIngredients implements Action {
  readonly type = ADD_INGREDIENTS;

  constructor(public payload: Ingredient[]) {}
}

// to fix the type error in the reducer
export type ShoppingListActions = AddIngredient | AddIngredients;
```
```TypeScript
// shopping-list/store/shopping-list.reducer.ts
import * as ShoppingListActions from './shopping-list.actions';

export function shoppingListReducer(
  state,
  action: ShoppingListActions.AddIngredient,
  // to use multiple change type
  // if we use just Action, another error with payload
  action: ShoppingListActions.ShoppingListActions
) {
  switch (action.type) {
    case ShoppingListActions.ADD_INGREDIENT:
      return {
        ...state,
        // the ingredient should be a part of an action. change later
        ingredients: [...state.ingredients, action]
      };
    case ShoppingListActions.ADD_INGREDIENTS:
      return {
        ...state,
        ingredients: [...state.ingredients, ...action.payload]
      };
  }
}
```

</details>

<details>
<summary>Dispatching the Actions</summary>

```TypeScript
constructor(private store: Store<...>) {}

this.store.dispatch(new ShoppingListActions.AddIngredient(newIngredient));
```
```TypeScript
// shopping-list.actions.ts
// change in AddIngredient
constructor(public payload: Ingredient) {}
```
- Angular will check all the reducers registered in app module and update the state according to the dispatched action

</details>

<details>
<summary>Setting up the Store</summary>

- have to tell Angular which reducers are involved and where to get them and store the state
```TypeScript
// app.module.ts
import { StoreModule } from '';
import { shoppingListReducer } from '';

@NgModule({
  // ...
  imports: [
    // ActionReducerMap is a JS object: id (any key name): reducer function
    StoreModule.forRoot({shoppingList: shoppingListReducer})
  ]
})
```

</details>

<details>
<summary>Using the state manager</summary>

- can also subscribe instead of using async pipe (but in that case need to unsubscribe)
```TypeScript
// shopping-list.component.ts
public ingredients: Observable<{ingredients: Ingredient[]}>;

constructor(
  // can't do it with Redux
  // but NgRx gives this ability (injectable store)
  // key as in .forRoot
  // Store from @ngrx/store
  // {} not the reducer, but the return value (the state like an init state)
  private store: Store<{shoppingList: {ingredients: Ingredient[]}}>
) {}

ngOnInit() {
  // selects the slice of a state
  // returns an Observable, no need to unsubscribe
  this.ingredients = this.store.select('shoppingList');
}
```
```HTML
<!-- shopping-list.component.html -->
<!-- use async pipe on view -->
<li *ngFor="let ingredient of (ingredients | async).ingredients">
```

</details>

<details>
<summary>Using one root state</summary>

- add store directive on app level and create there a reducer
```TypeScript
// app.reducer.ts
import {ActionReducerMap} from '@ngrx/store';
import * as fromShoppingList from '';
import * as fromAuth from '';

export interface AppState {
  shoppingList: fromShoppingList.State;
  auth: fromAuth.State;
}

export const appReducer: ActionReducerMap<AppState> = {
  shoppingList: fromShoppingList.shoppingListReducer,
  auth: fromAuth.authReducer
};
```

</details>

<details>
<summary>What are side effects?</summary>

- effects are things in the app, which don't affect the state while running and don't need to immediately update the state
- ex. http requests (result matters) when we start sign-up process, this is not important (split into 2-3 actions: start sign-up, sign-up success, sign-up error)
- the request is not something our store/state cares about, only the result, so it's just some side-effect code we run
- the same is for localStorage, though it runs sync and theoretically we could use it inside the reducer but it's a bad practice, it doesn't affect our state, it won't break the app (as an async code will) but still a bad practice, because it's just a side effect of the application
- things like that when the result matters but the process not are side effects

</details>

<details>
<summary>Using the NgRx Effects</summary>

- `npm install --save @ngrx/effects`
- gives a place to manage the side effects in between dispatching actions
- basically you can still manage side effects using services and reducers to manage the state

</details>

<details>
<summary>Define the Effect</summary>

- add `auth.effects.ts` to the store directive
- `Actions` here are is different from `Actions` of `@ngrx/store` package
- here we don't change the state but manage all the other code related to dispatched actions
- `actions$` is a stream of dispatched actions
- `ofType` operator is not a part of `rxjs`, it's provided by `@ngrx/effects` - allows to define a filter for which types of actions you want to continue in this observable pipe you're creating, this observable stream here because you can have multiple effects by adding multiple props to your class here and you can simply define different types of effects that you want to handle in each chain
- just returning an observable won't work in the effect
- an effect by default should always return a new action
- effect itself doesn't change the state
- but when it's done we want to change the state
- `@Effect()` to turn the method into an effect `@ngrx/effects` could be able to pick up later (required for `ngrx/effects` to pick up this method as an effect) to subscribe and so on
- have to return a new action at the end of the chain
```TypeScript
// auth.effects.ts
import {switchMap} from 'rxjs/operators';
import {Actions} from '@ngrx/effects';
import * as AuthActions from './auth.actions';

// to be able to inject things here
// or there would be an error
// don't add providedIn: 'root'
// because we're not going to inject it elsewhere
@Injectable()
export class AuthEffects {
  // effects are added as a normal prop of a class
  // don't subscribe here, @ngrx/effects will subscribe
  // just call the pipe
  @Effect()
  authLogin = this.actions$.pipe(
    // need to pipe a special ngrx operator
    // can pass several actions
    // filters to chain only when the action is LOGIN_START type,
    // all other actions will not trigger the effect
    ofType(AuthActions.LOGIN_START),
    // allows to create a new observable by taking
    // another observable's data
    switchMap((authData: AuthActions.LoginStart) => {
      // need to return an observable
      return this.http.post(...).pipe(
        // if no error - use map
        map(resultData => {
          // return from inside the pipe new action
          // no need to dispatch, will automatically be treated
          // as an action by @ngrx/effects and will be dispatched
          return new AuthActions.Login(...);
        }),
        catchError(error => {
          // ...
          // have to return a non-error observable
          // of creates a new observable w/o an error
          return of(new AuthActions.LoginFail(errorMessage));
        })
      );
    }),
    // but we want to login user only if we don't have an error
    // observable completes when the error is thrown, observable dies
    // for actions$ we can't stop the observable, it's an ongoing stream
    // otherwise the login won't work after the error is thrown
    // so can't add the catchError here
    // or not to add at all and request throws an error, actions$ will die
    // have to call the pipe on inner observable
    catchError()
  );
  // one big observable, that will give the access to
  // all the dispatched actions so that you can react to them
  // just react differently than in the reducer
  constructor(private actions$: Actions) {}
}
```
- add new action to actions
```TypeScript
// auth.actions.ts
// the point where we want to start sending our request
export const LOGIN_START = '[Auth] Login Start';
export const LOGIN_FAIL = '[Auth] Login Fail';

export class LoginStart implements Actions {
  readonly type = LOGIN_START;

  constructor(public payload: {email: string; password: string}) {}
}

export class LoginFail implements Actions {
  readonly type = LOGIN_FAIL;

  constructor(public payload: string) {}
}
```
- fix the reducer
```TypeScript
export interface State {
  // ...
  authError: string;
}

const initialState = {
  // ...
  authError: null
};

// and add the logic to the reducer function for all the actions
```
- register effects in the AppModule
```TypeScript
// app.module.ts
import {EffectsModule} from '@ngrx/effects';

@NgModule({
  imports: [EffectsModule.forRoot([AuthEffects])]
})
```
- subscribe to the state in `ngOnInit` of the component
```TypeScript
this.store.select('auth').subscribe(authState => {
  this.isLoading = authState.loading;
  this.error = authState.authError;
})
```
- but where to redirect the user?
- in `OnInit` there could be strange scenarios
- navigation could also be seen like a side effect
- add a new effect for successful login
- and this effect won't dispatch an action `@Effect({dispatch: false})` will not yield a dispatchable action at the end

</details>

<details>
<summary>Using the effect in a resolver</summary>

- the resolver expects an observable as a return value on the resolve method and waits for the observable to complete before it loads the route
- but when we dispatch an action, we don't get back the observable, so the resolve would instantly resolve and we will instantly resolve the route when the data is not there yet
- can fix with using effects
```TypeScript
export class RecipesResolverService implements Resolve<Recipe[]> {
  constructor(
    private store: Store<fromApp.AppState>,
    private actions$: Actions
  ) {}

  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot) {
    // can't return an action, it doesn't yield the observable
    this.store.dispatch(new RecipesActions.FetchRecipes());
    // have to wait the effect triggered by this action to complete
    // actions$ could be used in any class and also w/o @Effect()
    return this.actions$.pipe(
      ofType(RecipesActions.SET_RECIPES),
      take(1)
    );
  }
}
```

</details>

<details>
<summary>Using the Store Devtools</summary>

- redux-devtools-extension (search)
- add to chrome / firefox
- `npm install --save-dev @ngrx/store-devtools`
- register tools in AppModule
```TypeScript
// app.module.ts
import {StoreDevtoolsModule} from '@ngrx/store-devtools';

@NgModule({
  // only log when in prod mode
  imports: [StoreDevtoolsModule.instruments({logOnly: environment.production})]
})
```
- open redux tool in devtools in the browser

</details>

<details>
<summary>The Router Store</summary>

- `npm install --save @ngrx/router-store`
- helps with reacting to router actions
- dispatches some actions automatically based on angular router
- will allow to run code in the reducer / effects when such a routing action occurs
```TypeScript
// app.module.ts
import {StoreRouterConnectingModule} from '@ngrx/router-store';

@NgModule({
  // .forRoot() empty
  imports: [StoreRouterConnectingModule.forRoot()]
})
```

</details>

<details>
<summary>Learn more</summary>

- [NgRx official](https://ngrx.io/docs)

</details>

## 20 - Offline

<details>
<summary>Learn more</summary>

- [Service Workers in Angular Official](https://angular.io/guide/service-worker-intro)
- [PWA Courses](https://academind.com/learn/progressive-web-apps/)

</details>

## 21 - Testing
<details>
<summary>Learn more</summary>

- [Angular Testing Official](https://angular.io/guide/testing)
- [Testing Components in Angular 2 with Jasmine](https://semaphoreci.com/community/tutorials/testing-components-in-angular-2-with-jasmine)
- [Ng Test CLI](https://github.com/angular/angular-cli/wiki/test)
- [Ng e2e CLI](https://github.com/angular/angular-cli/wiki/e2e)

</details>

## 22 - Debugging
<details>
<summary>Notes</summary>

- find an error in the console
- using sourcemaps and breakpoints in browser
  - `sources` => `webpack` => `.` => `src`
- using `debugger;`
- using chrome extension Augury (access from dev tools)

</details>

## Deploy

<details>
<summary>What files do you deploy?</summary>

- after building the app for production the contents of `dist/my-project-name` is meant to be uploaded to the serve

</details>

<details>
<summary>Order</summary>

1. Use and check environment variables
2. Polish the code
3. `ng build --prod` uses ahead-of-time compilation
4. Deploy built artifacts (generated files) to static host (because it's only html css and js)
  - static host means it can run only html, css and js logic, not backend

</details>

<details>
<summary>Environment variables</summary>

- built-in feature in every Angular project
- `environments` directive may have several files
  - the name of the exported constant is the same
  - can add there API keys for different modes
  - for production Angular automatically swaps `environment.ts` => `environment.prod.ts`
  - to use just import where needed `import { environment } from '../environment/environment'` (don't add .prod here, Angular swaps those files automatically for different modes)

</details>

<details>
<summary>Deployment example (Firebase hosting)</summary>

1. build the project for production `ng build --prod`
2. need a static website host
  - AWS
  - Firebase hosting (don't need to have backend here also)
3. install firebase CLI -g (node.js and npm required)
4. `firebase login`
5. `firebase init` to connect the project to firebase project
6. add only `hosting` (other features if needed) here database is in case we use the firebase CDK for that but we already have firebase database setup (works without CLI already)
7. choose the project to connect
8. set public directory to `dist/ng-complete...`
9. configure as an SPA? y - to be sure that all the requests sent to the API will be redirected to the `index.html` (have to config the server so that it always hit the `index.html`, no matter what path is in the browser) but by default server is set to different path requests and if the url is unknown to the server => error, we have router but it's only client side and runs only if the server serves the request, so all the requests should be redirected to the `index.html` and since any request reaches this page, Angular router can load the content via router
10. do not overwrite `index.html`
11. run `firebase deploy`

</details>

<details>
<summary>Learn more</summary>

- [How to fix broken Routes after Deployment](https://academind.com/learn/angular/angular-q-a/#how-to-fix-broken-routes-after-deployment)

</details>

## Animations

<details>
<summary>General info</summary>

- with Angular animations we can animate different states of DOM elements with triggers
- can also animate from `void` (when there is no element in the DOM) to when the element is added to the DOM
- can use keyframes in animations
- can also run several animations at once (with `group`)

</details>

<details>
<summary>Learn more</summary>

- [Docs: Introduction to Angular animations](https://angular.io/guide/animations)

</details>

## PWA
<details>
<summary>Learn more</summary>

- [Docs: Angular service worker introduction](https://angular.io/guide/service-worker-intro)

</details>

## Schematics
<details>
<summary>Learn more</summary>

- [Generating code using schematics](https://angular.io/guide/schematics)

</details>

## 25 - Universal
<details>
<summary>General info</summary>

- used to pre-render Angular pages on the server
- when the app is loaded and runs on the client, it's a normal SPA again
- server-side rendering (SSR) can make sense because of SEO considerations (crawler should see what your users see) or because you want to deliver a finished page to your users (rather than creating the page in the browser)
- but that also has one important implication: you MUST NOT use any browser-only APIs like `document.querySelector()` in your Angular code! 
- simply because it will execute on the server and there such APIs are not available
- that's why it's better to use Angular features only: these features are safe to use because Angular will check if a certain API can be used before it uses it

</details>

<details>
<summary>Learn more</summary>

- [Angular Universal Official](https://angular.io/guide/universal)

</details>

## 26 - Angular Elements
<details>
<summary>General info</summary>

- allows to load a component dynamically as a native web component
- Angular Elements allows to turn Angular components into native Web Components
  - Web Components are part of JS DOM API, not related to Angular
- good thing to use if we want to insert Angular components into HTML
- allows to dynamically insert HTML code holding Angular Components after the Angular App has been compiled and loaded
  - app is compiled ahead-of-time and with JiT compilation it is also compiled before the content is loaded
- for now can be used only in Angular Projects

</details>

## 26 - Updating Angular
<details>
<summary>Learn more</summary>

- [Update Official](https://update.angular.io/)
- [Version 9 of Angular Now Available — Project Ivy has arrived!](https://blog.angular.io/version-9-of-angular-now-available-project-ivy-has-arrived-23c97b63cfa3)
- [Angular 9 - What's New? What changed?](https://www.youtube.com/watch?v=TcdhAxDWWxM&feature=youtu.be)

</details>

## Useful resources
<details>
<summary>Articles</summary>

- [x] [Setting the title, meta, work with location, access DOM, @Attribute decorator for performance and more](https://blog.bitsrc.io/10-useful-angular-features-youve-probably-never-used-e9e33f5c35a7)

</details>