---
title: "Dependency Injection Tricks in Angular"
date: 2020-06-04T10:31:03+02:00
draft: false
description: Tips how dependencies can be provided in parent components / directives or attached directives.
slug: dependency-injection-tricks-in-angular
tags: ["angular", "dependency-injection"]
---

{{< figure src="/images/dependency-injection-tricks-in-angular.jpg" alt="Dependency Injection Tricks in Angular" >}}

Here are few tricks that I picked up along the way in everyday **Angular** use and study. Along with usual provideIn:{} and dependency
injection from documentation examples, there is as usual - more to the story. 

### Providing dependencies - the alternate ways.

#### Declaring the suspects: 
1. A service that will be the dependency we are injecting: **LoggerService**
2. Parent component that will provide service
3. Directive: **ProvideDirective** that will also provide aforementioned service.
4. Child component that will use the service which will be provided to it in 2 different ways.

Ok with that out ot the way let us start:

#### Declaring LoggerService
{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "demo-logger.service.ts" >}}
Nothing much here just a simple service that logs stuff.

#### Component that will provide service
{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "dep-injection-parent.component.ts" >}}
Inside `providers: [LoggerService]` we will provide service so it can be injected in this components children later.

#### Directive that also provides the service
{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "provide.directive.ts" >}}
This directive will be attached to component later and thus the component will also have access to the service.

#### Child component consuming the dependencies
{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "dep-injection-child.component.ts" >}}
The Gist above just injects the service and it has no idea who is providing it. It also injects parent component so we can log it later
in our message.

#### Putting it in action
{{< gist NFantela 89298e327de9c8ab75a68d7e02676aba "dep-inj-tricks.demo.ts" >}}
Here we can see `<dep-child-comp>` appearing two times and no errors. The service is provided in both cases. In first case it is provided by the parent component
and in the last from attached directive.


#### Stackblitz demo for the example above:
[Dependency Injection tricks in Angular on Stackblitz](https://stackblitz.com/edit/dependency-injection-tricks-in-angular)