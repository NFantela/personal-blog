---
title: "Fixing Circular Imports in Angular using Injection Tokens"
date: 2020-06-01T13:31:03+02:00
draft: true
description: A quick fix to prevent Circular Imports error in Angular using Injection tokens.
slug: fixing-circular-imports-in-angular-with-injection-tokens
tags: ["angular", "typescript", "dependency-injection"]
---
This is not something directly related to **Angular** but programming in general.
Most common use cases involve parent directive/component querying for children via [@ContentChildren()](https://angular.io/api/core/ContentChildren)  and later on those same child components injecting aforementioned parent. 

### Let us set up our suspects
