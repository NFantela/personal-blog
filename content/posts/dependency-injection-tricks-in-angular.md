---
title: "Dependency Injection Tricks in Angular"
date: 2020-06-03T13:31:03+02:00
draft: true
description: Tips how dependencies can be provided in parent components / directives or attached directives.
slug: dependency-injection-tricks-in-angular
tags: ["angular", "dependency-injection"]
---
{{< figure src="/images/dependency-injection-tricks-in-angular.jpg" alt="Dependency Injection Tricks in Angular" >}}

{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "demo-logger.service.ts" >}}

{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "dep-injection-parent.component.ts" >}}

{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "dep-injection-child.component.ts" >}}

{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "provide.directive.ts" >}}

{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "dep-inj-tricks.demo.ts" >}}


#### Stackblitz demo for the example above:
[Dependency Injection tricks in Angular on Stackblitz](https://stackblitz.com/edit/dependency-injection-tricks-in-angular)