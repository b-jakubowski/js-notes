# Angular-Interview-Questions

## Table of Contents
Architecture:
* [Model-View-Presenter with Angular](#model-view-presenter-with-angular)
* [Component based architecture](#component-based-architecture)
* [Dependency injection](#dependency-injection)
* [Unidirectional data flow](#dependency-injection)
* [Centralized state management](#centralized-state-management)

General:
* [Components life-cycle hooks](#Components-life-cycle-hooks)
* [One-way and Two-way Data Binding in Angular](#one-way-and-two-way-data-binding-in-angular)
* [Performance Optimizations](#performance-optimizations)

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

NgRx:
* [What is NgRx](#what-is-ngrxs)

TypeScript: 
* [TypeScript inference type](#typescript-inference-type)

Testing:
* [JavaScript & Node.js testing best practices](https://github.com/goldbergyoni/javascript-testing-best-practices)



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
