[Accueil](README.md) [Commandes Git](Git.md) [TypeScript](Typescript.md)

## Spread operator (...)

- ### Application sur les objets

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

- ### Application sur les Array

```ts
const objA = [1, 4, 5];
const objB = [...objA, 6];
console.log(objB);
```

```json
[1, 4, 5, 6]
```

## Tri

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

- ### Tri de string sans modifier la collection originale

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

## Distinct sur un array

```ts
[...new Set([0, 1, 1, 2, 2])];
```

```json
[0, 1, 2]
```

## Destructuration d'objets

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

## Manipulation avancée des types

- ### Omit

```ts
type typeA = {
  prop1: number;
  prop2: string;
  prop3: number;
};

type typeB=Omit<typeA,'prop2'>;

const ObjtypeB:typeB={
    prop1:132,
    prop2:'ddd'; <== Error : Object literal may only specify known properties, but 'prop2' does not exist in type 'typeB'.
}

```

- ### Exclude (travail sur les union types)

```ts
type typeA = 'Test'| 12 | 4;

type typeB=Exclude<typeA,12>;
const a:typeB=4;
const b:typeB='Test';
const c:typeB=12; <== Error : Type '12' is not assignable to type 'typeB'
```

## Types avancés

- ### Créer un type avec toutes les propriétées readonly à partir d'un autre type

```ts
  type MyReadonly<T> = {
    readonly [k in keyof T]: T[k];
  };
  type typeA={
    prop1:number;
    prop2:string;
    prop3:number;
  }
  const objA: MyReadonly<typeA> = {
    prop1: 123,
    prop2: "test",
    prop3: 456,
  };

  objA.prop1 = 456; <== Error : champ readonly
```
- ### Fonction qui dépend d'un type générique avec condition sur le type
```ts	
type typeA = {
  amount: number;
  prop2: string;
  prop3: number;
};

const ObjtypeA: typeA = {
  amount: 132,
  prop2: "test",
  prop3: 456,
};

function doubleAmountValue<T>(
  value: T extends { amount: number } ? T : never
): T {
  return { ...value, amount: value.amount * 2 };
}
const doubleValueA=doubleAmountValue(ObjtypeA);
const doubleValueB=doubleAmountValue({ prop3: 456 });<== Error : Type 'number' is not assignable to type 'never'
```	
