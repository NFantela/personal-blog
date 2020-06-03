---
title: "Multiple inheritance with Typescript and class mixins"
date: 2020-06-01T11:31:03+02:00
draft: false
description: Add multiple inheritance to JS class using mixins and typescript.
slug: multiple-class-inheritance-in-typescript-with-mixins
tags: ["typescript", "OOP"]
---

{{< figure src="/images/multiple-class-inheritance-in-typescript-with-mixins.jpg" alt="Multiple inheritance with Typescript & Mixins" >}}

### The Problem : extending more than 1 class in Typescript
This is common use case scenario in OOP hovewer in Typescript & Javascript a slight hack is required.

### The solution: Mixins
Are functions that return class constructors so let us dive into example:

#### Mixin file
{{< gist NFantela b4766f59ebcf6f10706b2073f47c2819 "mixins.ts" >}}
In the Gist above, we first declare **Class Constructor** type that will implement our interfaces which will basically define types (class) constructors that will be returned (Disabled, HasValue).
Next we declare **mixin functions** themselves. In both cases same thing occurs, we implement different interface and set the corresponding property (isDisabled / value) to the new class constructor.

#### Using mixin in an angular component class
{{< gist NFantela b4766f59ebcf6f10706b2073f47c2819 "mixin-demo.component.ts" >}}
Above the component definition we first declare BaseClass that will be passed to our mixin functions. 
Next we  declare const _MixinDemoBase that has our mixin type constraints (DisabledCtor & HasValueCtor & typeof MixinDemoBase) and stores returning value from mixin function calls.
After that we extend our component with _MixinDemoBase and implement interfaces Disabled, HasValue so the typescript in template can pick up our 2 new props. Take note how we mark  inputs: ['isDisabled', 'value'], in our component metadata so we can pass values to those props when using component.

#### Putting it all together
We pass values to both inputs. 
{{< gist NFantela b4766f59ebcf6f10706b2073f47c2819 "final.component.ts" >}}


### Stackblitz demo for example above:
[Multiple inheritance with Typescript demo app](https://stackblitz.com/edit/multiple-inheritance-with-mixins?file=src%2Fapp%2Fapp.component.ts)
