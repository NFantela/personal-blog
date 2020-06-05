---
title: "Rebuilding Typescript utility types"
date: 2020-06-05T11:31:03+02:00
draft: true
description: Learning how typescript utility types work under the hood by reconstructing them.
slug: rebuilding-typescript-utility-types
tags: ["typescript"]
---

{{< figure src="/images/rebuilding-typescript-utility-types.jpg" alt="Rebuilding Typescript utility types img" >}}

If like me you ever wondered how to recreate some Typescript magic yourself the following tips are for you. There are many utility types
so we will narrow down to some interesting ones.

### Utility types we will reconstruct
1) Partial<T>
2) Readonly<T>
3) Pick<T,K>
4) Exclude<T,K>
5) Extract<T,K>
5) NonNullable<T>

Things to note in the following examples is first : that typescript removes *never* so bascicaly
`type MyCustomType = string | never | boolean;` will equal to **string | boolean**. Second : You should realy take time
to study Conditional Types it is worth it :).


#### Partial and Readonly
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "partial-and-readonly.ts" >}}


#### Pick
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "my-pick.ts" >}}

#### Exclude and Extract
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "exclude-and-extract.ts" >}}


#### NonNullable
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "my-non-nullable.ts" >}}



#### Stackblitz demo for our custom types:
[Rebuilding Typescript utility typesdemo on Stackblitz](https://stackblitz.com/edit/rebuilding-typescript-utility-types)
