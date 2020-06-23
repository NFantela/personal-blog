---
title: "Rebuilding Simple NGRX Store clone part one"
date: 2020-06-30T10:08:03+02:00
draft: true
description: Deconstructing NGRX store to small workable demo.
slug: rebuilding-simple-ngrx-store-clone-pt-one
tags: ["angular", "ngrx"]
---

{{< figure src="/images/rebuilding-simple-ngrx-store-clone.jpg" alt="Rebuilding Simple NGRX Store" >}}

> Second part of this tutorial and full stackblitz demo on: 
> [Rebuilding Simple NGRX Store clone part two](https://niksa-fantela.com/rebuilding-simple-ngrx-store-clone-pt-two)

## Just the core we need to get the store going.

Angular s NGRX store is big so we will stick to the core we need to get our simple store clone running. In the process we will use
and examine NGRX store's original code. We will omit things like runtime checks and meta reducers and just focus on the following:

### Elements we need

1) Store 
-- is a class extending **Observable and Observer** that puts the state as its observable source.
Connects all the below elements and has action dispatcher method 
  *dispatch()*. Also selects slices of state with *select()* method.

2) Actions 
-- we have action creator functions and ActionsSubject class that extends BehaviorSubject<Action> and
provide us with stream containing currently dispatched action string.

3) Reducers 
-- consists of reducer creator functions and ReducerManager class also extending  BehaviorSubject<ActionReducer<any, any>> 

4) State 
-- like ActionsSubject also a class extending BehaviorSubject<>. It takes in ActionsSubject stream, 
   and ReducerObservable stream

5) Store Module 
- for simplicity we will just cover StoreModule.forRoot, not features.

### Kicking off with actions and action creators
We will use ngrx models.ts file to have access to all cool types and interfaces we will need. I suggest studying Typescript Conditional types if this file seems like "vodoo" :).

### Ngrx Store dispatch action flow
Core workflow with store is **making** it change (actions) and using (displaying) its state via streams. 
**Store class** dispatch() calls next on **ActionsSubject** ->
In **State class** where we listen to this stream combined with ReducerManager stream this triggers a call to *reduceState()* fn
that takes in this new action and state and then returns a new state.

#### Action creator
{{< gist NFantela 4b53b848de69c5122b9aff61c204d813 "action-creators.ts" >}}
From the Gist above we can see createAction() fn with 3 overloads meaning it can be called in 3 ways:
1) Type only `createAction('[Counter] Increment')`
2) With additional metadata `createAction('[Auth/API] Login Success', props<{ user: User }>() );`
3) With a Fn that will be run: `createAction('[Auth/API] Login Success',(response: Response) => response.user`;

#### ActionsSubject
{{< gist NFantela 4b53b848de69c5122b9aff61c204d813 "action-subject.ts" >}}
We extend BehaviorSubject and make sure that the object of Action type is always passed to next() call.

### The Reducers
Time to move to the morst important part of the store - **reducers**;

#### The On s
{{< gist NFantela 7ef8b940a2ba2fc69671c1784077dde4 "reducer_creator.ts" >}}

The On function takes in *ActionCreator* (up to 10 based on its overloads) and last param is always reducer Fn *OnReducer*
that takes in state and action and returns a new state. 
The return type of On looks like `{ reducer: Function; types: string[] }` meaning that it will combine type strings (one or more) with the reducer function. 
This gives us the flexibility of using multiple action types (strings) with the same reducer fn.

#### Time to create reducer
The first param is always the current state all others are results of *on()* calls that are spread in  an array.
This fn is a closure that will *remember* a map that will hold key as action type and the value will be a reducer. Take note
that the type (key in our map) is always **unique** so when it is found have it  just calls its existing reducer Fn (value in map)
to create a new state for our new reducer.

#### Reducer Manager - the BehaviorSubject class
{{< gist NFantela 7ef8b940a2ba2fc69671c1784077dde4 "reducer_manager.ts" >}}
At this point we need *Injection tokens* so we will add them from the ngrx tokens.
Since they will be provided in module file here in ReducerManager they are injected to provide us with reducers.
We will also add utils.ts from the ngrx store with needed functions e.g. `combineReducers`.


This is arguably the most complex part of the store after it gets easier.

In the `constructor()` of ReducerManager class the following is happening. 
1)  ` private dispatcher: ReducerManagerDispatcher` The dispatcher is ActionsSubject with different provider alias
2)  The `INITIAL_STATE` token  from store module if not provided in config will be `{}`
3)   `@Inject(INITIAL_REDUCERS) private reducers: ActionReducerMap<any, any>,` Reducers can be provided 
in  `StoreModule.forRoot({ game: fromScoreboard.reducer })` or via @Injection tokens
4)  `@Inject(REDUCER_FACTORY) private reducerFactory: ActionReducerFactory<any, any>`
     We will not use metaReducers. If config.reducerFactory is not provided combineReducers fn will be passed  as first argument  looking like createReducerFactory(combineReducers, [])
       this will return a function that takes reducers and initial state.
This function will immediately be called in constructor {...} `super(reducerFactory(reducers, initialState));` meaning it will be the first thing in our BehaviourSubject extended class.
Other methods are for managing adding / removing of reducers.

#### We will end the first part with reducers and continue on the link below:

> Second part of the above tutorial and full stackblitz demo: 
> [Rebuilding Simple NGRX Store clone part two](https://niksa-fantela.com/rebuilding-simple-ngrx-store-clone-pt-two)