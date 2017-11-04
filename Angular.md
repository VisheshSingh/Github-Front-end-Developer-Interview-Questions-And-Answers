# How do you transition between two states:
```
  animations: [
    trigger('heroState', [
      state('inactive', style({
        backgroundColor: '#eee',
        transform: 'scale(1)'
      })),
      state('active',   style({
        backgroundColor: '#cfd8dc',
        transform: 'scale(1.1)'
      })),
      transition('inactive => active', animate('100ms ease-in')),
      transition('active => inactive', animate('100ms ease-out'))
    ])
  ]
  ```
# How do you define a wildcard state?
```
* => *
* => active
```

# What does this line do:

```ts
@HostBinding('class.valid') isValid;
```

Binds a host element property (here, the CSS class valid) to a directive/component property (isValid).

# What would be a good use for NgZone service?

The most common use of this service is to optimize performance when starting a work consisting of one or more asynchronous tasks that don't require UI updates or error handling to be handled by Angular. Such tasks can be kicked off via runOutsideAngular and if needed, these tasks can reenter the Angular zone via run.

# Why would you use renderer methods instead of using native element methods?

You are not sure what the context you are doing the rendering. You might be assuming the browser compilation and native DOM methods to be available but that might not be the case. It is better to be safe and let Angular handle the manupulation for elements.
The Renderer is a class that is a partial abstraction over the DOM. Using the Renderer for manipulating the DOM doesn't break server-side rendering or Web Workers (where direct access to the DOM would break).

ElementRef is a class that can hold a reference to a DOM element. This is again an abstraction to not break in environments where the browsers DOM isn't actually available.
Permitting direct access to the DOM can make your application more vulnerable to XSS attacks. Carefully review any use of ElementRef in your code. For more detail, see the Security Guide."

"Use this API as the last resort when direct access to DOM is needed. Use templating and data-binding provided by Angular instead. Alternatively you take a look at Renderer which provides API that can safely be used even when direct access to native elements is not supported."

# What is a good use case for ngrx/store?

Here is a great talk that goes into detail of the problems ngrx solving to manage state in applications by [Victor Savkin](https://twitter.com/victorsavkin?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor): https://www.youtube.com/watch?v=brCGZ8Lk-HY&t=1245s

# Can you talk about a bug related to a race condition, how to solve it and how to test it?

You can find the answer of this question in detail in this article: https://blog.nrwl.io/rxjs-advanced-techniques-testing-race-conditions-using-rxjs-marbles-53e7e789fba5

# What is the minimum definition of a component?
Component decorator allows you to mark a class as an Angular component and provide additional metadata that determines how the component should be processed, instantiated and used at runtime.

Components are the most basic building block of an UI in an Angular application. An Angular application is a tree of Angular components. Angular components are a subset of directives. Unlike directives, components always have a template and only one component can be instantiated per an element in a template.

# What is the difference between a component and a directive?

Component will have the template but directive wont. 
Basically there are three types of directives in angular2 according to documentation.

     Component
    Structural directives
    Attribute directives
* Component

is also a type of directive with template,styles and logic part which is most famous type of directive among all in angular2. In this type of directive you can use other directives whether it is custom or builtin in the @component annotation 

* Structural directives

like *ngFor and *ngIf used for changes the DOM layout by adding and removing DOM elements. explained here

* Attribute directives

are used to give custom behaviour or style to the existing elements by applying some functions/logics. like ngStyle is a attribute directive to give style dynamically to the elements. we can create our own directive and use this as Attribute of some predefined or custom elements

# How do components communicate with each other?

    1)Using @Input, @Output and EventEmitter
    
    2)Using Services and injecting them
# How do you create two way data binding in Angular?
    1) By using both Property binding and Event Binding both together at a time.
    2) By using [(ngModel)]     

# What does a lean component mean to you?

ased on the Angular Overview on application architecture, a component should be lean, and contain only the logic to control a view. It should not fetch data from the server, or validate user input, but should delegate any such task to a service.

A component's job is to enable the user experience and nothing more. It mediates between the view (rendered by the template) and the application logic (which often includes some notion of a model). A good component presents properties and methods for data binding. It delegates everything nontrivial to services.
A service, on the other hand, is a specific piece of logic that can be reused multiple times throughout your application. It helps keep your components lean, and your application DRY.

Service is a broad category encompassing any value, function, or feature that your application needs.

Almost anything can be a service. A service is typically a class with a narrow, well-defined purpose. It should do something specific and do it well.

# What would you consider a thing you should be careful doing on ngOnInit()?
Implement this interface to execute custom initialization logic after your directive's data-bound properties have been initialized. ngOnInit is called right after the directive's data-bound properties have been checked for the first time, and before any of its children have been checked. It is invoked only once when the directive is instantiated.
ngOnInit is a life cycle hook called by Angular2 to indicate that Angular is done creating the component.
# What is the differance between ngOnInit() and class constructor?
Constructor : constructor is a default method runs (by deafult) when component is being constructed. When you create an instance of a class that time also constructor(default method) would be called. So in other words, when component is being constructed or/and an instance is  created constructor(default method) is called and relevant code written within is called. Basically and generally in Angular2 it used to inject things like services when component is being constructed for the further use.

OnInit: ngOnInit is component's life cycle hook which runs first after constructor(default method) when component is being initialized.

# What is the purpose of NgModule?

NgModule helps us to organize our components, directives and services into a logical unit, each focused on a feature.

For example, we have 5 components in your project and that each component is dependent on other component or services or pipes then we need to import them into the respective component. And, then repeat the same process for all other components. This will become cumbersome to keep including on each of these components. This is where NgModules recuse us by importing everything to @NgModule which will be available throughout the components under one module.

# How do you decide to create a new NgModule?

When we are dealing with medium or large apps, it includes discrete set of functionality. Administration, Dashboard, Bookings/Orders, Promotions are all examples of areas of our apps that, when linked together, make our app. We basically breakdown our app into smaller pieces called Features / Modules.

In the process of developing an app we might create a feature which we don't want to expose or create a feature which we want to lazy loading when the user decides it is time to revisit the feature. NgModules helps us to separate our features to logical units and load it when required.

# What are the attributes that you can define in an NgModule annotation?
Declare which components, directives, and pipes belong to the module.
Make some of those classes public so that other component templates can use them.
Import other modules with the components, directives, and pipes needed by the components in this module.
Provide services at the application level that any application component can use.
The metadata imports a single helper module, BrowserModule, which every browser app must import.

BrowserModule registers critical application service providers. It also includes common directives like NgIf and NgFor, which become immediately visible and usable in any of this module's component templates.

The declarations list identifies the application's only component, the root component, the top of the app's rather bare component tree.

# what is Compile ahead-of-time (AOT)? differance between it and JIT?

Consider the static alternative which can produce a much smaller application that launches faster, especially on mobile devices and high latency networks.

In the static option, the Angular compiler runs ahead of time as part of the build process, producing a collection of class factories in their own files. Among them is the AppModuleNgFactory.

The syntax for bootstrapping the pre-compiled AppModuleNgFactory is similar to the dynamic version that bootstraps the AppModule class.
* Compile just-in-time (JIT)

In the first, dynamic option, the Angular compiler compiles the application in the browser and then launches the app.

# What is the difference between a module's forRoot() and forChild() and forFeature()
 methods and why do you need it?
* forRoot creates a module that contains all the directives, the given routes, and the router service itself.
* forChild creates a module that contains all the directives and the given routes, but does not include the router service.

RouterModule also offers a forChild static method for configuring the routes of lazy-loaded modules.

forRoot and forChild are conventional names for methods that configure services in root and feature modules respectively.

Angular doesn't recognize these names but Angular developers do. Follow this convention when you write similar modules with configurable service providers.

# What would you have in a shared module?

Create a SharedModule with the components, directives, and pipes that you use everywhere in your app. This module should consist entirely of declarations, most of them exported.

The SharedModule may re-export other widget modules, such as CommonModule, FormsModule, and modules with the UI controls that you use most widely.

The SharedModule should not have providers for reasons explained previously. Nor should any of its imported or re-exported modules have providers. If you deviate from this guideline, know what you're doing and why.

Import the SharedModule in your feature modules, both those loaded when the app starts and those you lazy load later.

# What would you not put shared module?====>providers
This question is addressed in the Why UserService isn't shared section of the NgModules page, which discusses the importance of keeping providers out of the SharedModule.

Suppose the UserService was listed in the module's providers (which it isn't). Suppose every module imports this SharedModule (which they all do).

When the app starts, Angular eagerly loads the AppModule and the ContactModule.

Both instances of the imported SharedModule would provide the UserService. Angular registers one of them in the root app injector (see What if I import the same module twice?). Then some component injects UserService, Angular finds it in the app root injector, and delivers the app-wide singleton UserService. No problem.

Now consider the HeroModule which is lazy loaded.

When the router lazy loads the HeroModule, it creates a child injector and registers the UserService provider with that child injector. The child injector is not the root injector.

When Angular creates a lazy HeroComponent, it must inject a UserService. This time it finds a UserService provider in the lazy module's child injector and creates a new instance of the UserService. This is an entirely different UserService instance than the app-wide singleton version that Angular injected in one of the eagerly loaded components.

# What module would you put a singleton service whose instance will be shared throughout the application (e.g. ExceptionService andLoggerService)?
* CoreModule

Create a CoreModule with providers for the singleton services you load when the application starts.

Import CoreModule in the root AppModule only. Never import CoreModule in any other module.

Consider making CoreModule a pure services module with no declarations

# What is the purpose of exports in a NgModule?
	
The confusion comes from the fact both Angular and ES6 are using the same terminology...

In ES6/TypeScript:

A module is any code file in your project.
An import is a line starting with the import keyword.
An export is a line starting with the export keyword.
In Angular:

A module is a class decorated with @NgModule. It serves as a registry (aka container) for all the components, pipes, directives and providers in your application.
An import is what you put in the imports property of the @NgModule decorator. It enables an Angular module to use functionality that was defined in another Angular module.
An export what you put is the exports property of the @NgModule decorator. It enables an Angular module to expose some of its components/directives/pipes to the other modules in the applications. Without it, the components/directives/pipes defined in a module could only be used in that module.
ES6 modules/imports/exports are very low-level. They are a feature of the ES6 language, just like keywords like const or let... In ES6/TypeScript, each file has ITS OWN SCOPE. So whenever you need to use a class/function/variable in a file and that class/function/variable was defined in another file, you must import it (the counterpart being that it must be exported in the file where it was defined). This is not specific to Angular. ALL PROJECTS WRITTEN IN ES6 can use modules/imports/exports in this manner.

On the other hand, Angular's modules/imports/exports are a feature of the Angular framework. They only make sense in Angular world. Other JavaScript frameworks might have similar notions but they'll use a different syntax.

# What is a pure pipe?
A pipe takes in data as input and transforms it to a desired output
# What is an async pipe?
The AsyncPipe accepts a Promise or Observable as input and subscribes to the input automatically, eventually returning the emitted values.

The AsyncPipe is also stateful. The pipe maintains a subscription to the input Observable and keeps delivering values from that Observable as they arrive.
# How do you create a custom pipe?
```
import { Pipe, PipeTransform } from '@angular/core';
/*
 * Raise the value exponentially
 * Takes an exponent argument that defaults to 1.
 * Usage:
 *   value | exponentialStrength:exponent
 * Example:
 *   {{ 2 | exponentialStrength:10 }}
 *   formats to: 1024
*/
@Pipe({name: 'exponentialStrength'})
export class ExponentialStrengthPipe implements PipeTransform {
  transform(value: number, exponent: string): number {
    let exp = parseFloat(exponent);
    return Math.pow(value, isNaN(exp) ? 1 : exp);
  }
}
```
# How does async pipe prevents memory leeks?

Async pipe knows about the lifespan of the component and unscubscribes from the observable if necessary.

#### What is the diffrence between RouterModule.forRoot() vs RouterModule.forChild()? Why is it important?

* forRoot creates a module that contains all the directives, the given routes, and the router service itself.
* forChild creates a module that contains all the directives and the given routes, but does not include the router service.
It registers the routers and uses the router service created at the root level.
* This is important because location is a mutable global property. Having more than one object manipulating the location is not a good idea.

#### How does loadChildren property work?

```ts
const routes: Routes = [
  ...,
  { path: 'edit', loadChildren: 'app/edit/edit.module#EditModule' },
  ...
]
```

* In the above example, loadChildren tells the router to fetch the EditModule bundle assigned to it *when* the user visits '/edit' url. (To be more precise, it will ask the module loader to find and load it.)
* Router will get the router configuration from edit module.
* It merges EditModule router configuration with the main application configuration.
* Activate all the needed components.

#### Do you need a Routing Module? Why/not?
Yes if the user was expected to navigate between different URLs. The Routing Module interprets the browser's URL as an instruction to load a specific component and its view. The application has to have its main router configured and bootstraped by passing an array of routes to `RouterModule.forRoot()`, and since this returns a module, it has to be added to the `imports` meta property in the main application module.

The RouterModule:

- separates our routing concerns from our feature module
- provides a module to replace or remove when testing our feature module
- provides a common place for require routing service providers including guards and resolvers
- is not concerned with feature module declarations

#### When does a lazy loaded module is loaded?

The `loadChildren` property is used by the Router to map to a bundle and lazy-load it. The router will take our `loadChildren` string and dynamically load in a module, add its routes as child routes to the configuration dynamically and then load the requested route. This will only happen when the route is first requested and the module will be immediately be available for subsequent requests.

Note that lazy-loaded modules should be removed from modules tehy were part of since they will be loaded on demand.


#### Below link doesn't work. Why? How do I fix it?

```html
<div routerLink='product.id'></div>
```

The routerLink should specify a defined path in the routing configuration and the required path parameter (`product.id`). The code above tries to visit a specific product page, so it should be done using *Link Parameters Array*:

```html
<div [routerLink]="['/product', product.id]"></div>
```

The above is correct in the case of having `product/:id` as a path in the application router configuration.


#### Can you explain the difference between ActivatedRoute and RouterState?

After the end of each successful navigation lifecycle, the router builds a tree of ActivatedRoute objects that make up the current state of the router. We can access the current RouterState from anywhere in our application using the Router service and the routerState property. 

RouterState is the current state of the router including a tree of the currently activated routes in our application along     convenience methods for traversing the route tree.

#### What is the use case of services?

The main use case of Services is to move duplicated code into a single location, acting like a Singleton. It encourages DRY (Don't Repeat Yourself), which is a principle in Software Engineering, aimed at reducing repitition of information or code in a multi-layered architecture.

Services can serve as a method of interaction between an application and a data store. It also can provide communication channels between directives, as well as any other business logic access.

#### How are the services injected to your application?

There are two ways to inject a service into your application:

- Per Application: Provides the service at an application level
- Per Component: Provides the service at a component level (and all child components)

Providing a service at an application level or a higher level creates a single instance of that service and shares it with all sub directives. This is useful in the case of sharing properties or state between service holders.

Providing a service for every different component would create an instance for each of the components with separate resources.

Injecting a service can be done by importing the service and specifying it in the `NgModule`'s metadata array preperty `providers`, and inject it into the directive using it via the constructor. To inject a service into another service, annotate the target service class with `@Injectable`.

```ts
//annotation used for services injecting other services
@Injectable()
export class MessageService {
	//injected service
	constructor(private errorService: ErrorService){}
}
```

#### How do you unit test a service with a dependency?
[insert answer]

#### Why is it a bad idea to create a new service in a component like the one below?

```ts
let service = new DataService();
```

That's a bad idea for several reasons including:

Our component has to know how to create a DataService. If we ever change the DataService constructor, we'll have to find every place we create the service and fix it. Running around patching code is error prone and adds to the test burden.

We create a new service each time we use new. What if the service should cache data and share that cache with others? We couldn't do that.

We're locking the component into a specific implementation of the DataService. It will be hard to switch implementations for different scenarios. Can we operate offline? Will we need different mocked versions under test? Not easy.


* What is a structural directive?


Structural directives are responsible for HTML layout. They shape or reshape the DOM's structure, typically by adding, removing, or manipulating elements.



* How do you identify a structural directive in html?


By the '*' before the directive name as in `<p *ngIf="true">`


* When creating your own structural directives, how would you decide on hiding or removing an element? What would be the advantages or disadvantages of choosing one method rather than the other? 


The difference between hiding and removing doesn't matter for a simple paragraph. It does matter when the host element is attached to a resource intensive component. Such a component's behavior continues even when hidden. The component stays attached to its DOM element. It keeps listening to events. Angular keeps checking for changes that could affect data bindings. Whatever the component was doing, it keeps doing.

Although invisible, the component—and all of its descendant components—tie up resources. The performance and memory burden can be substantial, responsiveness can degrade, and the user sees nothing.

On the positive side, showing the element again is quick. The component's previous state is preserved and ready to display. The component doesn't re-initialize—an operation that could be expensive. So hiding and showing is sometimes the right thing to do.

But in the absence of a compelling reason to keep them around, your preference should be to remove DOM elements that the user can't see and recover the unused resources with a structural directive like NgIf .


# What pseudo-class selector targets styles in the element that hosts the component?
:host

Use the :host pseudo-class selector to target styles in the element that hosts the component (as opposed to targeting elements inside the component's template).

# How would you select all the child components' elements?

# How would you select a css class in any ancestor of the component host element, all the way up to the document root?
:host-context

Sometimes it's useful to apply styles based on some condition outside of a component's view. For example, a CSS theme class could be applied to the document <body> element, and you want to change how your component looks based on that.

Use the :host-context() pseudo-class selector, which works just like the function form of :host(). The :host-context() selector looks for a CSS class in any ancestor of the component host element, up to the document root. The :host-context() selector is useful when combined with another selector.

The following example applies a background-color style to all <h2> elements inside the component, only if some ancestor element has the CSS class theme-light.
```
:host-context(.theme-light) h2 {
  background-color: #eef;
}
```

# What is <ng-container>?

 A grouping element that does not interfere with styles or layout (it's analogous to curly braces in JavaScript).Angular doesn't put it in the DOM.
 
 <ng-container> is a logical container that can be used to group nodes but is not rendered in the DOM tree as a node.

<ng-container> is rendered as an HTML comment.
So ng-container is useful when you want to conditionaly append a group of elements (ie using *ngIf="foo") in your application but don't want to wrap them with another element.
```
<div>
    <ng-container *ngIf="true">
        <h2>Title</h2>
        <div>Content</div>
    </ng-container>
</div>
```
will then produce :
```
<div>
    <h2>Title</h2>
    <div>Content</div>
</div>
```
https://blog.angular-university.io/angular-ng-template-ng-container-ngtemplateoutlet/


## Template Syntax Questions

**What is a template reference variable, and how would you use it?**

A: A variable (defined using a #) in a component template, which can be referenced in other parts of the template. For example, a template variable for a form can then be referenced by other elements of the form.

**What are the possible ways to bind component properties to an associated template?**

A: Interpolation binding, one way binding, two way binding.

**What does the ngFor template syntax look like?**

A: example:`<ul><li *ngFor="let val of values">{{val}}</li></ul>`

**What does the pipe syntax look like in Angular templates?**

A: example: `<div>{{ value | my-pipe : option }}</div>`

**What does an interpolated string look like in a template?**

A: example: `<div title="Hello {{username}}">...</div>`

**What is `<ng-container>`?**

A: A grouping element that does not interfere with styles or layout (it's analogous to curly braces in JavaScript).


**What is `<ng-template>`?**

A: It's an Angular element for rendering HTML when using structural directives. The ng-template itself does not render to anything but a commment directly.


## Component/Directive Questions

**What is the minimum definition of a component?**

A: A class with a Component decorator specifying a template.

**What is the difference between a component and a template?**

A: A component is a directive with a template (representing a view).

**What are different kinds of directives supported in Angular 2?**

A: Structural, component, and attribute directives.

**How do components communicate with each other?**

A: Various ways - for example: Input/Output properties, services, ViewChild/ViewContent.

**How do you create two way data binding in Angular 2.0?**

A: By using the two-way binding syntax [()] (along with ngModel, if you're doing this in the context of a form control element).

**How would you create a component to display error messages throughout your application?**

A: Implement your own ErrorHandler and configure it in the list of providers for the modules you want it used in. 

**How would you support logging in your Angular app?**

PA: One way would be to use angular2-logger, which is a package inspired by log4j. 

**How would you use the ngClass directive?**

A: For example: `<div [ngClass]="{firstCondition: 'class1', secondCondition: 'class2'}">...</div>`

**How do you resolve a template URL relative to a Component class?**

A: By specifying the moduleId to be module.id in the Component decorator. (Note: while this is still needed when using SystemJS, it is not necessary anymore when using Webpack module bundler for Angular 2 projects.)


## NgModules Questions:

**What is the purpose of NgModule?**

A: It's to give Angular information on a particular module’s contents, through decorator properties like: declarations, imports, exports, providers, etc.

**How do you decide to create a new NgModule?**

A: Typically for a nontrivial feature in an application, that will involve a collection of related components and services.

**What are the attributes that you can define in an NgModule annotation?**

A: Declarations, imports, exports, providers, bootstrap

**What is the difference between a module's forRoot() and forChild() methods and why do you need it?**

A: forRoot and forChild are conventional names for methods that deliver different import values to root and feature modules.

**What would you have in a shared module?**

A: Common components, directives, and pipes used in other modules in your application.

**What would you not put shared module?**

A: Services that should not have multiple instances created for the application.

**What module would you put a singleton service whose instance will be shared throughout the application (e.g. ExceptionService andLoggerService)?**

A: Root Module

**What is the purpose of exports in an NgModule?**

A: Provide components, directives, pipes to other modules for their usage.

**Why is it (potentially) bad if SharedModule provides a service to a lazy loaded module?**

A: You will have two instances of the service in your application, which is often not what you want.

**Can we import a module twice?**

A: Yes, and the latest import will be what is used.

**Can you re-export classes and modules?**

A: Yes.

**What kind of classes can you import in an angular module?**

A: Components, pipes, directives

## Services Questions:

**What is the use case of services?**

A: One very common use case is providing data to components, often by fetching it from a server. Though there’s no real definition of service from Angular point of view – it could do almost anything (e.g., logging is another common use case, among many).

**How are the services injected to your application?**

A: Via Angular’s DI (Dependency Injection) mechanism

**Why is it a bad idea to create a new service in a component like the one below?**

`let service = new DataService();`

A: The object may not be created with its needed dependencies.

**How to make sure that a single instance of a service will be used in an entire application?**

A: Provide it in the root module.

**Why do we need provider aliases? And how do you create one?**

A: To substitute an alternative implementation for a provider.  Can create like so: `{ provide: LoggerService, useClass: DateLoggerService }`


## Lifecycle Hooks Questions:

**What is the possible order of lifecycle hooks in Angular?**

A: ngOnChanges, ngOnInit, ngDoCheck, ngAfterContentInit, ngAfterContentChecked, ngAfterViewInit, ngAfterViewChecked, ngOnDestroy.

**When will ngOnInit be called?**

A: Called once, after the first ngOnChanges.

**How would you make use of onNgInit()?**

PA: Fetch initial component data (e.g. from server).

**What would you consider a thing you should be careful doing on onNgInit()?**

A: You cannot expect the component's children's data-bound properties to have been checked at this point.

**What is the difference between onNgInit() and constructor() of a component?**

A: A directive’s data-bound input properties are not set until after construction, so that’s one difference.

## Pipes Questions:

**What is a pure pipe?**

A: A pipe that is only executed when Angular detects a pure change to the input value (e.g. new primitive object or new object reference).

**What is an impure pipe?**

A: A pipe that is executed during every component change detection cycle (i.e., often – every keystroke, mouse move).

**What is an async pipe?**

A: An impure pipe that accepts a promise or observable as input and eventually returns emitted values.

**What kind of data can be used with async pipe?**

A: Stateful, asynchronous

**What types of pipes are supported in Angular 2?**

A: Pure and impure pipes (async pipes a kind of impure pipe).

## Routing Questions:

**What is the difference between RouterModule.forRoot() vs RouterModule.forChild()? Why is it important?**

A: forRoot is a convention for configuring app-wide Router service with routes, whereas forChild is for configuring the routes of lazy-loaded modules.

**How does loadChildren property work?**

A: The Router calls it to dynamically load lazy loaded modules for particular routes.

**When does a lazy loaded module get loaded?**

A: When its related route is first requested.

**How would you use a Route Guard?**

A: You would implement CanActivate or CanDeactivate and specify that guard class in the route path you’re guarding. 

**What are some different types of RouteGuards?**

A: CanActivate, CanDeactivate, CanLoad, Resolve, etc.

**How would you intercept 404 errors in Angular 2?**

A: Can provide a final wildcard path like so: { path: ‘**’, component: PageNotFoundComponent }

**This link doesn't work. Why? How do I fix it?**
`<div routerLink='product.id'></div>`

A: `<a [routerLink]=”[’product.id’]”>{{product.id}}</a>`


**What do route guards return?**

A: boolean or a Promise/Observable resolving to boolean value.

**What is <router-outlet> for?**

A: Place where routes are mounted in the app??


## Styling Questions:

**How would you select a custom component to style it?**

A: Using the `:host` pseudo-class selector in your component's styles.

**How do you reference the host of a component?**

A: Let DI inject an ElementRef into the constructor of your component.

**What pseudo-class selector targets styles in the element that hosts the component?**

A: The :host pseudo class selector.

**How would you select all the child components' elements?**

A: With the @ViewChildren decorator, like for example:

`@ViewChildren(ChildDirective) viewChildren: QueryList<ChildDirective>;`

**How would you select a css class in any ancestor of the component host element, all the way up to the document root?**

A: Using the :host-context() pseudo-class selector.

**What selector force a style down through the child component tree into all the child component views?**

A: Use the /deep/ selector along with :host pseudo-class selector.

**What does :host-context() pseudo-class selector target?**

A: The :host-context() selector looks for a CSS class in any ancestor of the component host element, up to the document root.

**What does the following css do?**
`:host-context(.theme-light) h2 {
  background-color: red;
}`

A: Will change this component’s background-color to red if the context of the host has the .theme-light class applied.


## Forms Questions:

**When do you use template driven vs model driven forms? Why?**

A: Template driven forms make more sense for simpler forms, at least in terms of validation. Model driven or Reactive forms lend themselves to easier testing of the validation logic, so if that’s complex, Reactive forms make more sense. There’s also the issue of asynchronous (template driven forms) vs. synchronous (model driven).

**How do you submit a form?**

PA: use the ngSubmit event binding like so: `<form (ngSubmit)="onSubmit()" …>`

**What's the difference between NgForm, FormGroup, and FormControl? How do they work together?**

A: FormGroup tracks the value and validity state of a group of AbstractControl instances. FormControl does the same for an individual control. NgForm is a directive that Angular automatically attaches to each `<form>` tag. It has its own ‘valid’ property which is true only if every contained control is valid.

**What's the advantage of using FormBuilder?**

A: Reduces repetition and clutter by handling details of control creation for you.

**How do you add form validation to a form built with FormBuilder?**

A: pass in Validator objects along with the FormControl objects...

**What's the difference between dirty, touched, and pristine on a form element?**

A: Dirty means it contains user data, touched means the user has at least done something with a particular control (perhaps just literally ‘touched’ it by giving it focus?), and pristine means the control has not been touched at all by the user.

**How can you access validation errors in the template to display error messages?**

PA: Use formErrors

**What is async validation and how is it done?**

A: Verifying some field using some asynchronous call (perhaps a server call)… return a `Promise<ValidationResult>` from your validator. When creating a FormControl object, you can pass an asynchronous validator into the constructor (e.g. `new FormControl(‘value’, syncValidator, asyncValidator)`).


**What is patchValue used for?**

A: Setting a form value (one or more fields with an object) bypassing validation.

## Animations Questions

**How do you define transition between two states?**

PA: Using the transition and animate function in an animations block like so: `animations: [transition('inactive => active'), animate('100 ms ease-in')]` 

**How do you define a wildcare state?**

A: Using the asterisk - example: `transition('* => active'), animate('100ms ease-in'))`

## Architecture / Framework Questions:

**What are some of the top level building blocks of the Angular framework?**

A: Services, Templates, Modules, Components, Providers, etc.

**What is AOT?**

A: Ahead of time compilation.

**What are some differences between Angular 2 and 4?**

A: Improvements in AOT; allowing else clause in ngIf, few other things...

**What are some security related features built in to the Angular framework?**

A: Sanitation, to prevent cross site scripting. Built-in support in the HttpClient to prevent cross-site request forgery.

**How can you bypass sanitation in Angular and why would you do so?**

A: To inject known safe code, you can bypass sanitation (e.g. to embed an iframe).

**What is a good use case for ngrx/store?**

A: Complex application state management requirements, involving asynchronous requests to update state.

**What is Redux and how does it relate to an Angular app?**

A: It's a way to manage application state and improve maintainability of asynchronicity in your application by providing a single source of truth for the application state, and a unidirectional flow of data change in the application. ngrx/store is one implementation of Redux principles.

**What would be a good use case for having your own routing module?**

A: An application whose requirements imply having many routes, and potentially route guards, and child routes.

**Where would you configure TypeScript specific compiler options for your project?**

A: In the tsconfig.json file.A

**What is the tslint.json file used for?**

A: Linting the TypeScript code (making sure it conforms to certain standards / conventions).

## API Questions:

**What does this line do?**
  `@HostBinding('[class.valid]') isValid;`

A: Applies the css class ‘valid’ to whatever is using this directive conditionally based on the value of isValid.

**Why would you use renderer methods instead of using native element methods?**

A: Potentially if you’re rendering to something besides the browser, e.g. rendering native elements on a mobile device, or server side rendering (?).

**What is the point of calling renderer.invokeElementMethod(rendererEl, methodName)?**

A: To invoke a method on a particular element but avoid direct DOM access (so we don’t tie our code just to the browser).

**How would you control size of an element on resize of the window in a component?**

A:
`@HostListener('window:resize', ['$event'])
onResize(event: any) {
    this.calculateBodyHeight();
}`

**What would be a good use for NgZone service?**

A: Running an asynchronous process outside of Angular change detection.

**How would you protect a component being activated through the router?**

A: Route Guards

**How would you insert an embedded view from a prepared TemplateRef?**

PA: `viewContainerRef.createEmbeddedView(templateRef);

## Testing Questions


**What is Protractor?**

A: E2E (end-to-end) testing framework.

**What is Karma?**

A: Unit test testing library.

**What are spec files?**

A: Jasmine unit test files.

**What is TestBed?**

A: Class to create testable component fixtures.

**What does detectChanges to in Angular jasmine tests?**

A: propagates changes to the DOM by running Angular change detection.

**Why would you use a spy in a test?**

A: To verify a particular value was returned or a method was called, for example when calling a service.


`

