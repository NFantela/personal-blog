---
title: "Bypassing ExpressionChangedAfterItHasBeenChecked Error in Angular"
date: 2020-06-05T10:31:03+02:00
draft: true
description: Most common error in Angular and simple ways of avoiding it.
slug: bypassing-ExpressionChangedAfterItHasBeenCheckedError-in-angular
tags: ["angular", "change-detection"]
---
{{< figure src="/images/bypassing-expressionchangedafterithasbeencheckederr-in-angular.jpg" alt="Bypassing ExpressionChangedAfterItHasBeenCheckedError in Angular img" >}}

ExpressionChangedAfterItHasBeenCheckedError is one of those things that if you are working with angular...You know.
Most often the correct way is to change **ngAfterViewInit** to **ngOnInit** lifecycle hook since ngAfterViewInit is run **AFTER** Angular has modified the **DOM**.
The most preffered way is to redesign your APP but if you have no choice a simple hack is the following.

### Making it Asynchronous
Since this **Angular check is run in dev mode and synchronously** we will be using microtask queue which is processed after all synchronous tasks.


#### Parent component
{{< gist NFantela d2c49ff23b2baa0a351931cce794a49c "main.errchanged.component.ts" >}}
This component will have 1 prop *text* which is updated via `update` method that will be called by child component ``emit()``.

#### Child component that will update parent 
{{< gist NFantela d2c49ff23b2baa0a351931cce794a49c "err-child.component.ts" >}}
Child component that receives parent s *text* prop and immediately in its ngOnInit lifecycle hook emits a new value which is then assigned in
parent via its `update` method thus triggering **ExpressionChangedAfterItHasBeenCheckedError** error. The reason this happens is covered in extensive articles 
by Max (link below) and is a story for itself. For now we will avoid the error by making our `this.changeParentProp.emit('updated text')` call **Asynchronous**.
As we see from the example this is done in 3 different ways - not using setTimeout :p.

1) Using `Promise.resolve().then(...)` 
2) Using `asyncScheduler.schedule(...)` basically same thing but can be used in streams if need arises.
3) Making `@Output() changeParentProp = new EventEmitter(true);` async by passing argument *true*


A Great article on [Angular Change Detection](https://indepth.dev/everything-you-need-to-know-about-change-detection-in-angular/)  by Max.

#### Stackblitz demo for the example above:
[Bypassing ExpressionChangedAfterItHasBeenCheckedError demo on Stackblitz](https://stackblitz.com/edit/bypassing-expressionchangedafterithasbeencheckederr-in-angular)