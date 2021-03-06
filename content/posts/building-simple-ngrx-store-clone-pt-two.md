---
title: "Rebuilding Simple NGRX Store clone part two"
date: 2020-07-09T10:31:03+02:00
draft: true
description: Deconstructing NGRX store to small workable demo.
slug: rebuilding-simple-ngrx-store-clone-pt-two
tags: ["angular", "ngrx"]
---
{{< figure src="/images/rebuilding-simple-ngrx-store-clone.jpg" alt="Rebuilding Simple NGRX Store" >}}

> First part of this tutorial series on: 
> [Rebuilding Simple NGRX Store clone part one](https://niksa-fantela.com/rebuilding-simple-ngrx-store-clone-pt-one)

Last time we finished with reducers now moving on to completing our simple store clone.

#### Adding State class
{{< gist NFantela 27f3c853a6e57ce8225c96295ad2c090 "state.ts" >}}

This class also Extending BehaviorSubject creates a stream that listens combines ActionsSubject and ReducerManager
into single stream that pushes new state to this class s .next() call.

Now come the methods we all know from the store like : *select()*and *dispatch()*.
**Select method** - so basicaly the store is a large nested object and using this method will allow to provide slices of its state e.g pick nested
object keys and get their values. This function comes in two variants for selecting slices of the state: First where 
a function is provided and second where property names (keys) are provided (up to 6 max).This function is declared outside  the Store class and is used inside the class with provided overloads. It returns 
**RxJS** operator function *selectOperator* that returns a stream being the result of selecting the pieces of the state object.
The **dispatch** is simple, by calling this method we are just providing next action to our actionsObserver this will force state change in State class stream.

## Check from here to below TODO :

#### The Store Module
Store module is needed to provide all this functionality. We will just focus on forRoot(). Inside StoreModule.forRoot() we see
the providers and factories that were used (and the correct order) to create reducers that were later used in *ReducerManager* class.

### Using our simple Ngrx store clone
First we need to create state and its corresponding interface. Then create 3 actions 
Now declare initial state and use *createReducer()* to **ActionReducerMap<DemoStoreState>** e.g. object
that will in our case look like : 
`{
  usersReducer : {
        users: [],
        selectedUser:{}
  }
}
`
Now in our app.module we import our clone store and register reducers:`StoreModule.forRoot(reducers)` and we can use it in app.component.
So inside ngOnInit() we select slices of the state using multiple object keys.
We dispatch actions to our store inside *handleUsrAction(...)*


#### Stackblitz demo for the example above:
[Simple NGRX Store clone](https://stackblitz.com/edit/simple-ngrx-store-recreation)