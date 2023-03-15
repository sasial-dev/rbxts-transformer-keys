# rbxts-transformer-keys
A roblox-ts transformer which enables to obtain keys of given type.

Forked from https://github.com/kimamula/ts-transformer-keys

# Requirement
TypeScript >= 3.4.1

# How to use this package

This package exports 2 functions.
One is `$keys` which is used in TypeScript codes to obtain keys of given type, while the other is a TypeScript custom transformer which is used to compile the `$keys` function correctly.

## How to use `$keys`

```ts
import { $keys } from 'rbxts-transformer-keys';

interface Props {
  id: string;
  name: string;
  age: number;
}
const keysOfProps = $keys<Props>();

console.log(keysOfProps); // ['id', 'name', 'age']
```

## How to use the custom transformer

```jsonc
// tsconfig.json
{
  "compilerOptions": {
    // ...
    "plugins": [
      { "transform": "rbxts-transformer-keys" }
    ]
  },
  // ...
}
```

# Notes

* The `$keys` function can only be used as a call expression. Writing something like `$keys.toString()` results in a runtime error.
* `$keys` does not work with type generics, i.e., `$keys<T>()` in the following code is converted to an empty array(`[]`).

```ts
class MyClass<T extends object> {
  keys() {
    // returns [] as generics do not work
    return $keys<T>();
  }
}
```

# License

MIT
