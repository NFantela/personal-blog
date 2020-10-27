---
title: "Recursion in Angular components"
date: 2020-10-27T10:01:03+02:00
draft: false
description: How to create tree like structures based on recursion in Angular.
slug: recursion-in-angular-components
tags: ["angular"]
---

{{< figure src="/images/recursion-in-angular-components.jpg" alt="How to create tree like structures based on recursion in Angular." >}}

On occassion we will need to use recursion to display some data (e.g. nested array structures). Luckily Angular components can be called from their
own template. Let us try it out:

### Simple recursion component
{{< gist NFantela 3956cb917ec45e935d186751952fd389 "simple-recursive.compnent.ts" >}}
This is basic recursion at work - we call component in its own template until we reach 0.

### More complex example - nested arrays
{{< gist NFantela 3956cb917ec45e935d186751952fd389 "array-recursive.component.ts" >}}
The most practical example is nested array structures that should be presented in **Tree like** structure. Here we check if current level 
is array or just item (string in our example). If it is array we loop over items and for each item render its own component. If we have just
a string we show it in template.

#### Stackblitz demo for this example:
[Recursion in Angular components on Stackblitz](https://stackblitz.com/edit/ang-recursive-component)

### Additional reading
For a more complex solution and in detail explanation - a great article : 
[Reusable Tree view Component](https://medium.com/its-tinkoff/lets-make-a-reusable-tree-view-component-in-angular-349eefc824d6)