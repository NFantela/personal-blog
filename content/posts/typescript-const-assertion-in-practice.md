---
title: "Typescript const assertions in practice"
date: 2021-02-26T09:11:03+02:00
draft: false
description: Narrowing down types with const assertion demo.
slug: typescript-const-assertions-in-practice
tags: ["typescript"]
---


With Typescript 3.4 we got  [const assertions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html).
Armed with this knowledge we can take a look at the following demo:

#### Fixating type with const assertion

{{< gist NFantela df0c3022d6e7492111abf99c49b7f341 "const-assertions-in-typescript.ts" >}}

First we declare our type : *Genres* that will be used to make a stronger type than string e.g. `'comedy' | 'horror'`.
In the demo above we can see that when we create an object (without declaring its type) firstBook, Typescript will infer genre
to string since no other information is provided. 

By attempting to use this object in our createCover() fn Typescript will yell at us since we are expecting an object whose genre is of type *Genres*
and we are giving it a string.

#### Const assertion to the rescue 
in *bestCaseFirstBook* we assert ` genre: 'comedy' as const` thus fixating the type of genre to 'comedy' and not string. Typescript can now
safely assume that type 'comedy' is found in *Genres* type and all is well. 















