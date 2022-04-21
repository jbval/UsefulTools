[Accueil](README.md) [Commandes Git](Git.md) [TypeScript](Typescript.md)

## Spread operator

- ### Objects

```ts
const objA = {
  prop1: 123,
  prop2: "test",
};
const objB = {
  ...objA,
  prop3: 456,
};
console.log(objB);
```

```json
{
  "prop1": 123,
  "prop2": "test",
  "prop3": 456
}
```

- ### Array

```ts
const objA = [1, 4, 5];
const objB = [...objA, 6];
console.log(objB);
```

```json
[1, 4, 5, 6]
```

## Sort

- ### number

```ts
const array = [1, 5, 2];
array.sort((a, b) => a - b);
console.log(array);
```

```json
[1, 2, 5]
```

- ### string

```ts
const array = ["aaa", "ccc", "bbb"];
array.sort((a, b) => a.localeCompare(b));
console.log(array);
```

```json
["aaa", "ccc", "bbb"]
```

- ### string copy

```ts
const array = ["aaa", "ccc", "bbb"];
const arrayB = [...array].sort((a, b) => a.localeCompare(b));
console.log(array);
console.log(arrayB);
```

```json
['aaa','ccc','bbb']
['aaa','bbb','ccc']
```

## Array Distinct

```ts
[...new Set([0, 1, 1, 2, 2])];
```

```json
[0, 1, 2]
```

## Destruct

```ts
const objA = {
  prop1: 123,
  prop2: "test",
  prop3: 456,
};
const { prop1, ...objBWithoutProp1 } = obj1;
console.log(prop1);
console.log(objBWithoutProp1);
```

```json
123

{
    prop2:'test',
    prop3:456
}
```

## Type Manipulation

- ### Omit

```ts
type typeA = {
  prop1: number;
  prop2: string;
  prop3: number;
};

type typeB=Omit<typeA,'prop2'>;

const ObjtypeB={
    prop1:132,
    prop2:'ddd'; <== Error
}

```

- ### Exclude

```ts
type typeA = 'Test'| 12 | 4;

type typeB=Exclude<typeA,12>;
const a:typeB=4;
const b:typeB='Test';
const c:typeB=12; <== Error
```
