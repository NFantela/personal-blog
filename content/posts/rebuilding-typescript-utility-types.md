---
title: "Rebuilding Typescript utility types"
date: 2020-06-09T11:31:03+02:00
draft: false
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
The above gist is simple we define a type where each key in passed type is marked
as optional by **?** or readonly with **readonly**.

#### Pick
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "my-pick.ts" >}}
 Creates a type with only picked keys that are passed as 2nd type argument, naturaly they must be
 existing keys of the main type passed as 1st argument.

#### Exclude and Extract
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "exclude-and-extract.ts" >}}
Here we use **Conditional Type** to figure out if second argument can extend first. If it does
in case of **MyExclude** we do not want it and return never (which is omitted by typescript).
**MyExtract** is just reversed **MyExclude**.
I have also applied these types in object type checks in examples *ObjWithExtract* and *ObjWithExclude*.

#### NonNullable
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "my-non-nullable.ts" >}}
This one is simple now.

#### Extract type from Array, Object or Flat (primitive) type
{{< gist NFantela 699bbbf0c7bc5b7938699a2bcdc4e2e1 "extract-type.ts" >}}



#### Stackblitz demo for our custom types:
[Rebuilding Typescript utility typesdemo on Stackblitz](https://stackblitz.com/edit/rebuilding-typescript-utility-types)
