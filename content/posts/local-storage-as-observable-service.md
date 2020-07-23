---
title: "Local storage as Observable Service"
date: 2020-07-23T10:08:03+02:00
draft: false
description: Creating a observable service from browser s local storage.
slug: local-storage-as-observabe-service
tags: ["angular", "rxjs"]
---
{{< figure src="/images/local-storage-as-observabe-service.jpg" alt="Creating a observable service from browser s local storage" >}}

A quick and simple example of creating a stream for your entire local storage. We will use an Observable based service. 

{{< gist NFantela f67dd75dd0a570b22b425eb277d2acd1 "local-storage.service.ts" >}}

Our service holds `_entireStorage$:BehaviorSubject<Map<string, string>>` subject that we will subscribe all users of this **service to in constructor**. This will handle multicasting. Other than that we have 3 very simple methods - adding and removing of items from local storage (these are public and can be used in components / directives using this service) and `_allStorage` that basicaly gathers entire storage into a map. This map is the data we store in our subject.

### Live Stackblitz demo of Observable local storage service.
[Local storage service](https://stackblitz.com/edit/local-stor-obs-service)