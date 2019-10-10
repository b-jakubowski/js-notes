# Tech-Interview-Questions

## Table of Contents
Basics:
* [Http](#http)
* [Graphql](#graphql)

Architecture:
* [Model-View-Presenter with Angular](#model-view-presenter-with-angular)
* [Component based architecture](#component-based-architecture)
* [Dependency injection](#dependency-injection)
* [Unidirectional data flow](#dependency-injection)
* [Centralized state management](#centralized-state-management)
* [What is bootstrapping](#what-is-bootstrapping)

OOP:
* [OOP encapsulation](#OOP-encapsulation)
* [OOP abstraction](#OOP-abstraction)
* [OOP inheritance](#OOP-inheritance)
* [OOP polymorphism](#OOP-polymorphism)
* [SOLID](#solid)
* [CLASS](#class)

General:
* [Components life-cycle hooks](#Components-life-cycle-hooks)
* [One-way and Two-way Data Binding in Angular](#one-way-and-two-way-data-binding-in-angular)
* [Performance Optimizations](#performance-optimizations)
* [Directives](#directives)
* [Http interceptors](#http-interceptors)
* [Services](#services)
* [Resolvers](#resolvers)

Routes:
* [Route Guards](#route-guards)
* [CanDeactivate guard](#candeactivate-guard)

RxJS:
* [Reactive programming](#reactive-programming)
* [Subject vs BehaviorSubject](#subject-vs-behaviorsubject)
* [Why use AsyncPipe](#why-use-asyncpipe)
* [RxJs Error Handling](#rxjs-error-handling)
* [Flattening operators](#flattening-operators)
* [Cache HTTP requests](#cache-http-requests)
* [When to unsubscribe](#when-to-unsubscribe)

NgRx:
* [What is NgRx](#what-is-ngrxs)

TypeScript: 
* [TypeScript inference type](#typescript-inference-type)

Testing:
* [JavaScript & Node.js testing best practices](https://github.com/goldbergyoni/javascript-testing-best-practices)


## Basics
### Http
* Communication between client computers and web servers is done by sending HTTP Requests and receiving HTTP Responses
* it is a client-server protocol, which means requests are initiated by the recipient, usually the Web browser. 
* client sends an HTTP request to the web -> web server receives the request -> The server runs an application to process the request -> The server returns an HTTP response (output) to the browser -> The client (the browser) receives the response

### Graphql
* GraphQL is a syntax that describes how to ask for data, and is generally used to load data from a server to a client
* only one endpoint for data exchanging.
* It lets the client specify exactly what data it needs.
* It makes it easier to aggregate data from multiple sources.
* It uses a type system to describe data.
* Resolvers specify where to take data from.
* Schema defines data types and structure.
* With GraphQL, the user is able to make a single call to fetch the required information rather than to construct several REST requests to fetch the same.


## Architecture:
### Model-View-Presenter with Angular
[More details](https://blog.angularindepth.com/model-view-presenter-with-angular-3a4dbffe49bb)
* Model-View-Presenter - architectural software design pattern for implementing the user interface (UI) of an application.
* Model-View-Presenter separates presentation layer from the domain model
* The presentation layer reacts to changes in the domain by applying the Observer Pattern
* The view does not contain any logic or behaviour except in the form of data bindings and widget composition. It delegates control to a presenter when user interactions occur.
* The presenter batches state changes so that the user filling a form results in one big state change as opposed to many small changes, e.g. update the application state once per form instead of once per field.

Components in that case can be divided :
- Presentational components - purely presentational and interactive views. They present a piece of the application state to the user and enable them to affect its state. keep the complexity of presentational components to an absolute minimum
- Container components - expose pieces of application state to presentational components. They integrate the presentational layer with the rest of our application by translating component-specific events to commands and queries for non-presentational layers.
- Mixed components -  they contain logic that belongs in multiple horizontal layers. complicated to reuse and tightly coupled.
![M-V-P](https://miro.medium.com/max/875/1*ZbBBKiBXGqVBYWwzbmZzNw.png "mvp")

### Component based architecture:
* Container components supply a data flow for presentation.
* Container components translate component-specific events to application state commands or actions to put it in Redux/NgRx Store terms.

### Dependency injection
* Dependency injection (DI) lets you keep your component classes lean and efficient. They don't fetch data from the server, validate user input, or log directly to the console; they delegate such tasks to services.

### Unidirectional data flow
change detection cannot cause cycles. It also helps to maintain simpler and more predictable data flows in applications, along with substantial performance improvements.
![unidirectional data flow](https://miro.medium.com/max/875/1*kwcTqvUDyhsPJU_Bbl4C6g.png "unidirectional data flow")

### Centralized state management
* The application state is a single immutable data structure
* A state change is triggered by an action, an object describing what happened
* Pure functions called reducers take the previous state and the next action to compute the new state

![state](https://miro.medium.com/max/875/1*KGK4Je5Iq7GrUPXz-XePzw.png "state")

### What is bootstrapping?
* An NgModule describes how the application parts fit together. Every application has at least one Angular module, the root module that you bootstrap to launch the application. By convention, it is usually called AppModule.
* bootstrap—the root component that Angular creates and inserts into the index.html host web page.
*  the bootstrapping process creates the component(s) listed in the bootstrap array and inserts each one into the browser DOM.
* Inserting a bootstrapped component usually triggers a cascade of component creations that fill out that tree of components.
* While you can put more than one component tree on a host web page, most applications have only one component tree and bootstrap a single root component.

## OOP
### OOP encapsulation
* it is the process of ensuring accurate protection over certain data (properties) passed back and forth between your application.
* **Private**: can only be accessed within the class it was defined in
* **Protected**: can only be accessed within the class it was defined in as well as inheriting the super class. Outside clients are unauthorized.
* **Getters**: its purpose is to give indirect read access to client code to a private or protected member that they are otherwise prohibited from. Read-only properties are made possible when used without it’s setter counterpart.
* **Setters**: its purpose is to give indirect write access to client code to a private or protected member that they are otherwise prohibited from. Write-only properties are made possible when used without it’s getter counterpart.

### OOP abstraction
* It is the process of hiding the internal complexity of a class while only requiring the absolute necessary data to function correctly.
* the goal is to make our source code as simple and easy to use as possible for our clients

### OOP inherirance
* the process of structuring a class hierarchy of similar objects that can extend the general functionality of it’s base while making it’s own implementation more concrete
* inheritance is the mechanism of basing an object or class upon another object (prototype-based inheritance) or class (class-based inheritance), retaining similar implementation.
* think in terms of base classes and sub classes when breaking down inheritance. Sub classes being the objects preforming the action of extending while base classes are the objects being extended.
*  Inheritance is very beneficial in keeping our code DRY compliant and happy side effect of this is that it helps to keep our file sizes small.

### OOP polymorphism
*  the condition of occurring in several different forms.
*  it is the ability for specific classes or objects to be referenced in their more general sense, to then preform an action shared amongst multiple sub types.
*  The big stipulation that comes with polymorphism, is that you cannot call any method specific to the sub class even if the variable that you’re dealing with is an instance of that sub class

### SOLID
[solid with typescript](https://medium.com/@ashu.singh212/s-o-l-i-d-in-typescript-c0e4fe6c345a)
* **Single responsibility principle**: a class should have one, and only one, reason to change;
You can apply the principle to methods or modules, ensuring that they do just one thing and therefore have just one reason to change.
* **Open-closed principle**: it should be possible to extend the behavoir of a class without  modifying it;
In short, inheritance fulfils the second principle.
* **Liskov Substitution principle**: Each derived class must replace its parent without affecting parent’s behaviour.
a subclass should override the parent class methods in a way that does not break functionality from a client’s point of view.
* **Interface segregation principle**: many small, client-specific interfaces are better than one general purpose interface;
In short, clients shouldn’t be forced to depend on methods they do not use.
* **Dependency inversion principle**: depends on abstractions not concretions;

### Class 
class is a blueprint for creating objects (a particular data structure), providing initial values for state (member variables or attributes), and implementations of behavior (member functions or methods).

### Object Oriented Programming
* OOP is usually defined by its two core concepts: Polymorphism and Inheritance.

## General

### Angular Performance Checklist
[Angular Performance Checklist](https://github.com/mgechev/angular-performance-checklist)
TLDR:
* OnPush strategy
* Angular Zone optimization
* manually set changeDetection
* @Input as setter instead OnChanges hook
* lazy loading of views / modules

### Server-side rendering
* A normal Angular application executes in the browser, rendering pages in the DOM in response to user actions. 
* Angular Universal executes on the server, generating static application pages that later get bootstrapped on the client. 
* SPA cannot be rendered until the entire JavaScript required for their initial rendering is available. This leads to two big problems:
1. Problems with dynamic content indexing by search-engines
1. User will see nothing more than a blank/loading screen until the JavaScript associated with the page is downloaded, parsed and executed.

### Components life-cycle hooks
* ngOnChanges() - Called before ngOnInit() and whenever one or more data-bound input properties change.
* ngOnInit() - Called once, after the first ngOnChanges().
* ngDoCheck() - Called during every change detection run, immediately after ngOnChanges() and ngOnInit().
* ngAfterContentInit() - Called once after the first ngDoCheck().
* ngAfterContentChecked() - Called after the ngAfterContentInit() and every subsequent ngDoCheck().
* ngAfterViewInit() - Called once after the first ngAfterContentChecked().
* ngAfterViewChecked() - Called after the ngAfterViewInit() and every subsequent ngAfterContentChecked().
* ngOnDestroy() - Called just before Angular destroys the directive/component.

### One-way and Two-way Data Binding in Angular
* One-way data binding will bind the data from the component to the view (DOM) or from view to the component. One-way data binding is unidirectional.
* Two-way data binding in Angular will help users to exchange data from the component to view and from view to the component. It will help users to establish communication bi-directionally.
* Why not 2-way-binding - what you lose in return is the ability to control when state should change and sight of where changes come from. Also when the application grows on size, the performance may decrease because angular will watch of every 2waybinding element.

### Performance Optimizations
[*article*](https://blog.angular.io/angular-tools-for-high-performance-6e10fb9a0f4a)


**Component level code-splitting** - load individual components lazily without a route navigation.
You can use: 
* [ngx-loadable](https://www.npmjs.com/package/ngx-loadable)
* [herodevs/hero-loader](https://www.npmjs.com/package/@herodevs/hero-loader)

**Route level code-splitting** - lazy load the individual routes.
[more about](https://web.dev/route-level-code-splitting-in-angular/)
* with Angular CLI v. 8.1 You can generate lazy module with `ng g module [module name] --route [route name] --module [parent module]`
this 

**Preloading Modules** - strategy that preloads all the modules in the application. You can use it by configuring the Angular router
`RouteModule.forRoot(ROUTES, { preloadingStrategy: PreloadAllModules })`.

For larger apps, that has many modules and requires advanced preloading:
* Quicklink — preload only modules associated with visible links in the viewport. [ngx-quicklink](https://github.com/mgechev/ngx-quicklink)
* Predictive prefetching — preload only the modules that are likely to be needed next [guess.js](https://github.com/guess-js/guess), [video guide](https://www.youtube.com/watch?v=5FRxQiGqqmM)

**Performance budget** - You can specify limits on production bundles of an app.
* If the budget’s `maximumWarning` value is reached, the CLI will show a warning.
* If the budget's `maximumError` value is reached the build will fail. 

### Directives
* is a function that executes whenever the Angular compiler finds it in the DOM.
* **Components** are just directives with templates. Under the hood, they use the directive API and give us a cleaner way to define them.
* **Attribute directives** manipulate the DOM by changing its behavior and appearance. use attribute directives to apply conditional style to elements. You can create custom ones like 'highlight'.
* **Structural directives** to create and destroy DOM elements. easy to recognize. An asterisk (*) precedes the directive attribute. `*ngIf`, `ngFor`
* Existing diractives examples `[ngClass]`

### Http interceptors
*  It provides a way to intercept HTTP requests and responses to transform or handle them before passing them along.
* Angular applies interceptors in the order that you provide them. If you provide interceptors A, then B, then C, requests will flow in A->B->C and responses will flow out C->B->A. You cannot change the order or remove interceptors later. 
USES:
* **Convert** - When the API returns a format we do not agree with, we can use an interceptor to format it the way we like it.
* **Manipulate URL** - We could, for example, want to change HTTP to HTTPS.
* **Global loader** 
* **Headers** - authentication, caching, 

### Services
* Components shouldn't fetch or save data directly and they certainly shouldn't knowingly present fake data. They should focus on presenting data and delegate data access to a service.
* @Injectable() decorator marks the class as one that participates in the dependency injection system.
* A component can delegate certain tasks to services, such as fetching data from the server, validating user input, or logging directly to the console. 
* **Singleton service** is a service for which only one instance exists in an app. You can creating by:
-> Declare root for the value of the @Injectable() providedIn property
-> Include the service in the AppModule or in a module that is only imported by the AppModule

### Resolvers
* Resolver is a service which has to be [provided] in root module
* resolver is that intermediate code, which can be executed when a link has been clicked and before a component is loaded.
* Route resolvers służy dostarczeniu danych do Routa, przed aktywacją Routa, a jeszcze prościej mówiąc, zmuszamy naszą aplikację, aby pokazał widok dopiero jak dane zostaną dostarczone.
* General routing flow
-> User clicks the link.
-> Angular loads the respective component.
* Routing Flow with Resolver
-> User clicks the link.
-> Angular executes certain code and returns a value or observable.
-> u can collect the returned value or observable in constructor or in ngOnInit, in class of your component which is about to load.
-> Use the collected the data for your purpose.
-> Now you can load your component.
```
	@Injectable()
	export class UserResolve implements Resolve<User> {
		constructor(private usersService: UsersService) {}

		resolve(route: ActivatedRouteSnapshot) {
			return this.usersService.getUser(route.params['id']);
		}
	}
```

## Rxjs
### Reactive programming: 
Angular uses RxJS to implement the Observable pattern.
An Observable is a stream of asynchronous events that can be processed with array-like operators.
- An Observer essentially subscribes to an Observable.
- The Observable then emits streams of data which the Observer listens and reacts to, setting in motion a chain of operations on the data stream.
- Operators allow you to transform, combine, manipulate, and work with the sequences of items emitted by Observables.

### Subject vs BehaviorSubject
A BehaviorSubject holds one value. When it is subscribed it emits the value immediately. A Subject doesn't hold a value.
- BehaviorSubject can be created with initial value: new BehaviorSubject(1)
- Consider ReplaySubject if you want the subject to hold more than one value

Subject example ():
```
const subject = new Subject();
subject.next(1);
subject.subscribe(x => console.log(x));
```
Console output will be empty

BehaviorSubject example:
```
const subject = new BehaviorSubject();
subject.next(1);
subject.subscribe(x => console.log(x));
```
Console output: 1

### Why use AsyncPipe
* less code. You dont have to subscribe in ts file to receive data.
* AsyncPipe autounsubcribes from observable. So there is again less code and performance enhancement(no memory leaks).

### RxJs Error Handling
* RxJs Operator, catchError is simply a function that takes in an input Observable, and outputs an Output Observable. if an error occurs, then the catchError logic is going to kick in
* It returns an replacement Observable for the stream that just errored out.
```
const http$ = this.http.get<Course[]>('/api/courses');

http$
    .pipe(
        catchError(err => of([]))
    )
    .subscribe(
        res => console.log('HTTP response', res),
        err => console.log('HTTP Error', err),
        () => console.log('HTTP request completed.')
    );
```
* `finalize` operator run code that we always want executed.
```
http$
    .pipe(
        map(res => res['payload']),
        catchError(err => throwError(err)),
        finalize(() => console.log("first finalize() block executed")),
```
* instead of rethrowing the error, we can also simply retry to subscribe to the errored out Observable.
```
http$.pipe(
        tap(() => console.log("HTTP request executed")),
        map(res => Object.values(res["payload"]) ),
        shareReplay(),
        retryWhen(errors => {
            return errors
                .pipe(
                    tap(() => console.log('retrying...'))
                );
        })
    )
    .subscribe()
```

### Flattening operators
based on [Demystifying Flattening Operators in RXJS without Code](http://alanpryorjr.com/2019-05-15-rxjs-flattening-operators/)
* **switchMap** - Drop everything you were already doing and immediately begin the new task. This means only the latest and greatest values are provided.
Commonly used with HTTP requests where a new source emission means you no longer care about or need the previous inflight request. The current inner observable is canceled and only the new one is active.

* **concatMap** - You add your boss’s request to the end of your to-do list, but you completely finish whatever you were currently working on, and then you begin work on the next task. You eventually finish everything, and you do so in order.
Use this when the order of operations is important such as if you were calculating updates to a financial transaction where you needed to add money and add an interest payment, in which case the order that the addition and multiplication happen matters and transactions occur in order.

* **mergeMap** - The overachieving multitasker. You immediately begin working on everything your boss gives you as soon as he/she assigns it.
use this when you don’t care about the order of operations and just want all of the things to happen ASAP, such as an alert system.

* **exhaustMap** - You have tunnel vision and completely ignore new requests from your boss until you are done with what you are working on, and only then do you begin listening for new tasks.
A common use-case here is login requests; usually there is no reason to send another authentication request until you have received the status of the first, so if the user types in their credentials and spammed the login button you would only send the first login request and not send another until it returns with success or failure.

### Cache HTTP requests
First, we just need to execute a regular HTTP query (for ex. get) and pipe the stream through shareReplay operator! This transforms the initial stream to a ReplaySubject! In other words, new subscriptions will NOT execute other HTTP requests but a cached value will be used  

### When to unsubscribe?
* inifinite observables (ex. with using interval())
* when using redux Store
* dont unsubscribe - async pipe
* dont unsubscribe - @HostListener
* dont unsubscribe - Usually when using http service 
be more declarative about unsubscribing
```
 ngOnInit() {
     this.todos = this.store.select('todos').takeUntil(this.componetDestroyed).subscribe(console.log); 

     this.posts = this.store.select('posts').takeUntil(this.componetDestroyed).subscribe(console.log); 
  }

  ngOnDestroy() {
    this.componetDestroyed.next();
    this.componetDestroyed.unsubscribe();
  }
```

## NgRx
### What is NgRx?
* NgRx provides state management, isolation of side effects, entity collection management, router bindings, code generation, and developer tools that enhance developers experience when building many different types of applications.
* Using NgRx Effects and Store, any interaction with external resources side effects, like network requests, web socket and any business logic can be isolated from the UI. This isolation allows for more pure and simple components, and keep the single responsibility principle.

## Routing
### Route Guards
* **CanActivate**: Controls if a route can be activated.
* **CanActivateChild**: Controls if children of a route can be activated.
* **CanLoad**: Controls if a route can even be loaded. This becomes useful for feature modules that are lazy loaded. They won’t even load if the guard returns false.
* **CanDeactivate**: Controls if the user can leave a route. Note that this guard doesn’t prevent the user from closing the browser tab or navigating to a different address. It only prevents actions from within the application itself.

### CanDeactivate guard

### TypeScript inference type
If you add value to initialized variable, there is no need to provide type to it
```
const x = 1;
```
there is no need to add `number` type to this case.
