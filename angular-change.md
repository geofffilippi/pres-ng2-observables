## Geoff Filippi

### Application Architect

---

# [Oildex](www.oildex.com)

A cloud service company for oil and gas

* 1 year

---

Formerly:

# [Time Warner Cable](www.timewarnercable.com)

* 12 years

---

## Experience

<i class="fa fa-phone"></i>

* Worked on streaming media (Voice over IP), 6 years
* 5 million phone customers

---

## Experience

<i class="fa fa-video-camera"></i>

* Worked on video and streaming video, 4 years

---

## Projects

[twctv.com](twctv.com)

* Video streaming website
 * backbone.js
* Video streaming Set-Top Box (STB) web application

---

## Oildex Projects

* Rewrite 10+-year-old apps
* Angular 1.4
 * New router
 * ES5
* No Angular 2, yet
* No ES6 or Typescript, yet

---

# We will cover

* Fundamentals
* Related concepts
* Angular 2

---

## Fundamentals

A _brief_ overview of reactive fundamentals

* Reactive programming
* Functional Reactive Programming (FRP)
* Observer design pattern

---

## Related concepts

* `Object.observe`
* Promises
 * Other Async concepts
* RxJS

---

## Observables in Angular 2

* Forms
* `Http`
* AsyncPipe

---

# Fundamentals

---

## Overview of Reactive Programming

* Data flows
* Propagation of change

---

## [Reactive Manifesto](http://www.reactivemanifesto.org)

* Responsive
* Resilient
* Elastic
* Message Driven

---

## (FRP) Functional Reactive Programming

* Reactive Programming

and

* Functional Programming

---

# Related Concepts

---

### Observer Design Pattern

* Subject tracks observers
* Subject notifies observers of state changes

---

### Terminology

* Subject, Observable, Producer
* Observer, Consumer

---

### [`Object.observe`](http://arv.github.io/ecmascript-object-observe/)

__Not the same as Observables__

* [Proposal withdrawn](https://esdiscuss.org/topic/an-update-on-object-observe)
 * Formerly a Stage 2 Proposal
* `Proxy`

---

### _Criticisms_ of `Object.observe`

* Big changes to Object internals
* Bad performance
* Not well-supported or adopted

_But really,_
* Ecosystem moved in different direction

---

## [`Observable`]()

* [Stage 1 Current Proposal](https://github.com/tc39/ecma262)
* [Description](https://github.com/zenparsing/es-observable)
* [Specification](https://zenparsing.github.io/es-observable/)

---

## Differences between Observables and `Object.observe`

---

## Creating an Observable

#### The hard way

```
let myObservable = new Observable(observer => {
  const token = doAsyncAction((err, value) => {
    if (err) }
      observer.error(err);
    } else {
      observer.next(value);
      observer.complete();
    }
  }); 

  return () => {
    cancelAsyncAction(token);
  };
{);
```

---

## Compare 

* Observables
* Promises
* Events
* callbacks

---

## [Promises vs. Observables](https://www.youtube.com/watch?v=zlERo_JMGCw)

* Promise is like a async variable
* Observable is like a async array

---

## [Promises vs. Observables](https://www.youtube.com/watch?v=KOOT7BArVHQ)

### Promises

* Single value
* Cannot be cancelled
* Not lazy
* Good for some AJAX calls
 * Unless you want to cancel them
* Catch, Finally

---

## Promises vs. Observables

### Observables

* Streams
* Can be unsubscribed
* Lazy, until you call `.subscribe()`
* Better for events, WebSockets
 * Animations, AJAX you want to cancel
* Can by retried
* Catch, Finally

---

### Bridging Observables

#### Easy way to get an observable

You can turn other async concepts into an observable using a helper

* Promises
 * `.from()`
* Generator
 * `.from()`
* Callbacks
 * `.fromCallback()`

---

### Bridging Observables

#### Easy way to get an observable

* Events
 * `.fromEvent()`
* DOM
 * AJAX
 * WebSockets `.fromWebSocket()`
* Other observable implementations
 * bacon.js
 * kefir.js

---

### Bridging Observables

You can even turn non-async concepts into an observable using a helper

* Arrays
 * `.of()`

---

## Working with Promises vs. Observables

* `.then()` becomes `.subscribe()`

---

## Working with Promises vs. Observables

Observables do not need to complete, but...

If you need to do something when an observable completes, pass an optional complete handler

---

## RxJS

* v5.0.0-beta.1
* Observable
* Subject
* Implementation used in Angular 2

---

# Angular 2

---

## Angular 2

* Forms
* `Http`
* AsyncPipe
* Change detection

---

## [Forms](http://blog.ng-book.com/the-ultimate-guide-to-forms-in-angular-2/)

Forms are observable

```
    this.myForm = fb.group({  
      'sku':  ['', Validators.required]  
    });

    this.sku = this.myForm.controls['sku'];

    this.sku.valueChanges.subscribe(  
      (value: string) => {  
        console.log('sku changed to: ', value);  
      }
    );

    this.myForm.valueChanges.subscribe(  
      (value: string) => {  
        console.log('form changed to: ', value);  
      }
    );
```

---

## [`Http`](https://auth0.com/blog/2015/10/15/angular-2-series-part-3-using-http/)

* Cancel requests
* Stream results
 * "type ahead"
* Returns observable

---

## [`Http`](https://auth0.com/blog/2015/10/15/angular-2-series-part-3-using-http/)

```
getRandomQuote() {
  this.http.get('http://localhost:3001/api/random-quote')
    .retry(3)
    .map(res => res.text())
    .subscribe(
      data => this.randomQuote = data,
      err => this.logError(err),
      () => console.log('Random Quote Complete')
    );
}
```

---

## Pipes

* Like Angular 1 `filter`

---

## [AsyncPipe](http://briantroncone.com/?p=623)

* Can subscribe to observables

```
timerAsync = Observable.interval(1000).startWith(0);
```

```
<h2>Current Total (Async Pipe): {{timerAsync | async}}</h2>
```

---

## [Change Detection](http://victorsavkin.com/post/110170125256/change-detection-in-angular-2)

New in Angular 2:

* Apps are reactive
* Change detection is directional
* You can skip walking parts of the tree
 * Immutable objects
 * Observables

---

## `ngrx`

Reactive Extensions for Angular 2

[`ngrx/store`](https://github.com/ngrx/store)

Can be used to implement elm/redux-style applications in Angular 2

---

# Questions?
