---
title: "Typescript custom error messages with Conditional types"
date: 2020-05-25T13:31:03+02:00
draft: false
description: Providing useful error messages to user when he types forbidden types in his code.
slug: typescript-custom-error-messages-with-conditional-types
tags: ["typescript"]
---
{{< figure src="/images/typescript-custom-error-messages-with-conditional-types.jpg" alt="Typescript custom error messages with Conditional types" >}}

Sometimes when building code that uses custom Types we want to limit those custom types e.g. give the developer some kind of custom
warning when he is trying to use our code. A good example is to create custom error type messages using **typescript conditional types.**

### Types...types everywhere..

#### Forbide Arrays and provide custom err message type
{{< gist NFantela 97ff5714cf6737c212315aecde35dc37 "simple-no-arrays.example.ts" >}}
In this simple Gist we first declare our conditional type **ArraysNotAllowed**. It will accept custom type and error message
type we want to display. By looking at `T extends any[]` we notice that if our custom type implements array type meaning if any type of
array is being passed it will immediately give back our error type warning otherwise it is the provided type.

#### Complex example using nested condition types
{{< gist NFantela 97ff5714cf6737c212315aecde35dc37 "complex-example.ts" >}}
A little more complex example. First we declare 2 error messages variables. Then we pull the types of those messages in *FunctionsNotAllowed* and *ValuePropertyNotAllowed* types.
Now comes the most important part, since we want to check for 2 types that are forbidden (Function and {value: any}) we need two conditional type checks lastly returning *unknown* "is the type-safe counterpart of any".
By this time we are ready to test this type with  3 calls to doSomething().

### Stackblitz demo for example above:
[Typescript custom error messages demo app](https://stackblitz.com/edit/typescript-custom-error-messages-with-conditional-types)