---
title: "Rebuilding Simple NGRX Store clone part one"
date: 2020-07-29T10:08:03+02:00
draft: true
description: Deconstructing NGRX store to small workable demo.
slug: rebuilding-simple-ngrx-store-clone-pt-one
tags: ["angular", "ngrx"]
---

@Directive({
   selector: '[waResizeObserver]',
   providers: [
       ResizeObserverService,
       {
           // a great way to pick up attribute from the template 
           // e.g. 
           // <div waResizeBox="content-box" > Resizable box </div>
           provide: RESIZE_OPTION_BOX,
           deps: [[new Attribute('waResizeBox')]],
           useFactory: boxFactory,
       },
   ],
})
export class ResizeObserverDirective {