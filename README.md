# Tech-Interview-Questions

## Table of Contents

* [Reactive programming](#reactive-programming)
* [Component based architecture](#component-based-architecture)
* [Dependency injection](#dependency-injection)

#### Reactive programming: 

Angular uses RxJS to implement the Observable pattern.
An Observable is a stream of asynchronous events that can be processed with array-like operators.
- An Observer essentially subscribes to an Observable.
- The Observable then emits streams of data which the Observer listens and reacts to, setting in motion a chain of operations on the data stream.
- Operators allow you to transform, combine, manipulate, and work with the sequences of items emitted by Observables.

#### AComponent based architecture:

* Container components supply a data flow for presentation.
* Container components translate component-specific events to application state commands or actions to put it in Redux/NgRx Store terms.

#### Dependency injection
* Dependency injection (DI) lets you keep your component classes lean and efficient. They don't fetch data from the server, validate user input, or log directly to the console; they delegate such tasks to services.
* Podstawową zasadą działania Dependency Injection jest posiadanie serwisu, który zajmuje się uzupełnianiem potrzebnych zależności.

#### Model-View-Presenter with Angular
[More details](https://blog.angularindepth.com/model-view-presenter-with-angular-3a4dbffe49bb)
* Model-View-Presenter (often abbreviated MVP) is an architectural software design pattern for implementing the user interface (UI) of an application.
* Model-View-Presenter separates presentation from the domain model
* The presentation layer reacts to changes in the domain by applying the Observer Pattern
* The view does not contain any logic or behaviour except in the form of data bindings and widget composition. It delegates control to a presenter when user interactions occur.
* The presenter batches state changes so that the user filling a form results in one big state change as opposed to many small changes, e.g. update the application state once per form instead of once per field.