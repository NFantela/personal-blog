---
title: "RxJS Observables Workout"
date: 2020-06-22T10:31:03+02:00
draft: true
description: Playing with different ways of RxJS Observables creation and usage.
slug: rxjs-observables-workout
tags: ["rxjs"]
---
{{< figure src="/images/rxjs-observables-workout.jpg" alt="Playing with different ways of RxJS Observables creation and usage" >}}

Using **RxJS** can make new devs and sometimes us experienced ones do "mind melt". The concepts seem so simple yet when put to action much confusion arises.
Needles to say I now love RxJs and creating new stream manipulations for my Angular Observables lead to greater satisfaction while coding.

To this end I have prepared some practice in different ways of creating **Observables.**

### Simple Observable 
{{< gist NFantela 6c2cc9713933d70912346ad91142b717 "easy-example.ts" >}}
In the gist above we create a new observable and provide **subscriber function**. Notice how inside the function something else (setInterval() in our case)
will push new values to the observer. The function returns **teardown logic**  that will also clear our interval.
 Observable<T> constructor be like:
` constructor(subscribe?: (this: Observable<T>, subscriber: Subscriber<T>) => TeardownLogic);`
 TeardownLogic is `{  unsubscribe(): void; } | Function | Void`
 Subscriber is object with  next(), complete(), error()

 The `(observerObj) => {...}` function in constructor is a subscriber function.

### Observable class that takes in another observable 
{{< gist NFantela 6c2cc9713933d70912346ad91142b717 "observable-in-observable.ts" >}}
What we see is basicaly same as in the first example only using class inheritance. We provide subscriber function this time in constructor *super()* call - we can now manipulate passed
observable in any way so we pluck props from the object and return new observable of those values. We
immediately **subscribe subscriber** (mind blown... :)) to the passed observable. The inner *.subscribe()* will return usual **subscription obj** that already **contains teardown logic**.

### Multicasting with Subjects
{{< gist NFantela 6c2cc9713933d70912346ad91142b717 "subject-in-observable.ts" >}}

This time the inner subject will be the source. We extend a class with Observable and use super() to call Observable constructor and make it multicast by using subjects by adding observerObj to list
of subject subscribers (this is simmilar as example above but instead of using passed  observables we use internal subject as our source.

### Creating custom operator
{{< gist NFantela 6c2cc9713933d70912346ad91142b717 "custom-rxjs-operator.ts" >}}
Finaly to top it all off and finish this *workout* we will create a custom operator that logs the stream value with optional custom message. Note that you can pass in other classes like *ngZone* in Angular etc.
The .lift call creates a new observable with passed operator.


### Stackblitz demo for example above:
[Observables in action](https://stackblitz.com/edit/rxjs-observable-workout)