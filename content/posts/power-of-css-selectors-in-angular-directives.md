---
title: "Power of Css selectors in Angular directives"
date: 2020-07-16T11:11:03+02:00
draft: false
description: Some nice  tricks while creating your Angular directives or components.
slug: power-of-css-selectors-in-angular-directives
tags: ["angular", "directives"]
---

{{< figure src="/images/power-of-css-selectors-in-angular-directives.jpg" alt="Circular Imports in angular" >}}

I was recently suprised on how cool you can actualy make your directive selectors in Angular by adhering to css selector rules. In this short example we will showcase the use of
`:not()`. Below is a simple example of two different
directives using basicaly *same selector*. Now we know we can attach multiple directives to same DOM node however in this case only second directive
would be rendered.

### Two different directive using the same selector?
We will bypass this rule by making our second directive use `CSS :not()` pseudo class selector.
{{< gist NFantela b15d709b057caccc677317027966d483 "some-example.directives.ts" >}}
First directive uses `@Input() someInput` so in our second directive me make sure that we avoid this element with `selector: 'some-directive:not([someInput])'`.

#### Using both directives in our HTML
{{< gist NFantela b15d709b057caccc677317027966d483 "same-selector.usage.html" >}}

Nice both are rendered in our DOM tree.