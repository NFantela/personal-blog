---
title: "Custom RXJS Operator : delayFirstEmmisionBy"
date: 2020-10-14T11:22:03+02:00
draft: false
description: Create custom RXJS operator to delay first emmision fron any observable.
slug: custom-rxjs-operator-delayfirstemmissionby
tags: ["rxjs"]
---

{{< figure src="/images/custom-rxjs-operator-delayfirstemmisionby.jpg" alt="Custom RXJS Operator  delayFirstEmmisionBy" >}}

I ran accross an use case when first emmision needed to be delayed by X seconds and therefore
had to resort to making my own custom operator.

### Take first emmision and then resubscribe
{{< gist NFantela 891a8eaf77aedeb23e27f2ecc11e5f26 "delay-first-emmision-by.ts" >}}