---
title: "Observable based preloading service"
date: 2020-08-17T10:55:03+02:00
draft: false
description: Custom preloading strategy that can be called anywere in Angular App listened by service implementing custom PreloadingStrategy.
slug: observable-based-preloading-service
tags: ["angular", "preloading"]
---
{{< figure src="/images/observable-based-preloading-service.jpg" alt="Observable based preloading service in Angular" >}}

Recently I came across on interesting Angular talk concerning **preloading of modules in Angular on demand**. By combining the power of
RxJs and Observable based services here is a solution that pre-loads modules from anywhere in Angular app using user events etc.

### NetworkAwarePreloadOnDemand service
{{< gist NFantela 5f0938be58c434b15b330f35285b0905 "network-aware-preloading.service.ts" >}}
Here we extend basic class implementing Angular s PreloadingStrategy interface with Observable. The observable connects 
subscriber of this class to inner private Subject. The subject is exposed as observable in our main method `preload()`. Inside the stream we stop
the stream first depending on network speed (if this is enabled via our InjectionToken PRELOAD_OPTIONS) and the second and final check is 
to see if the current route is the one that is demanded `_shouldPreload()`. If both filters pass we pre-load the route.

### Adding strategy to routes inside module
{{< gist NFantela 5f0938be58c434b15b330f35285b0905 "preload-service-app.module.ts" >}}
We provide our Service as any other Preloading strategy.

### Pre loading the modules on mouse click
{{< gist NFantela 5f0938be58c434b15b330f35285b0905 "network-app.component.ts" >}}
First we inject the service and then call `addPreloadOption()` method on our service that checks and adds the route to inner subject.That
event starts the stream logic.
####
[Preload Strategies in Angular on ng-conf](https://www.youtube.com/watch?v=rr5whHCdVCY)
#### Stackblitz demo for this preloading service:
[Rebuilding Typescript utility typesdemo on Stackblitz](https://stackblitz.com/edit/observable-preloading-strategy-service)