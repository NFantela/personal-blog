---
title: "Fixing Circular Imports in Angular using Injection Tokens"
date: 2020-05-10T13:31:03+02:00
draft: false
description: A quick fix to prevent Circular Imports error in Angular using Injection tokens.
slug: fixing-circular-imports-in-angular-with-injection-tokens
tags: ["angular", "typescript", "dependency-injection"]
---

{{< figure src="/images/fixing-circular-imports-in-angular-with-injection-tokens.jpg" alt="Circular Imports in angular" >}}

This is not something directly related to **Angular** but programming in general.
Most common use cases involve parent directive/component querying for children via [@ContentChildren()](https://angular.io/api/core/ContentChildren)  and later on those same child components injecting aforementioned parent. 

### Let us set up our suspects

There are three things we will need: 

1. **Injection token** and **interface**
2. **Parent directive** that will be used as element here (not attribute selector):
 `<parent-dir>... child components here... </parent-dir>` . 
The directive will gather children via @ContentChildren and update their props as proof we can use them. 
3. **Children components** that will inject (via constructor) aforementioned parent directive and display its prop in their template. 
Take note at this point we would have a circular import error if we were injecting the directive directly. 

First we set up interface to represent our parent directive and corresponding injection token:

{{< gist NFantela f99be01b8429470642e80770ed68c1e5 "circular-imports.ts" >}}

Now we declare parent directive that will provide **itself** under the declared token:

{{< gist NFantela f99be01b8429470642e80770ed68c1e5 "parent.directive.ts" >}}

The child components are now ready to inject parent directive

{{< gist NFantela f99be01b8429470642e80770ed68c1e5 "child.component.ts" >}}

And finally putting it to test: 

{{< gist NFantela f99be01b8429470642e80770ed68c1e5 "app.component.ts" >}}

#### Stackblitz demo for the example above:
[Circular imports in Angular on Stackblitz](https://stackblitz.com/edit/fixing-circular-imports-demo?file=src%2Fapp%2Fapp.component.ts)

