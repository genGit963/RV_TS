# Type Inference

**Type Inference** in TypeScript refers to the language’s ability to automatically determine the types of variables, function return types, or expressions based on the values assigned to them. TypeScript tries to infer as much as it can from the code, reducing the need for explicit type annotations while still maintaining type safety.

## Key Concepts of Type Inference:

1. **Basic Variable Inference**
2. **Function Return Type Inference**
3. **Contextual Typing**
4. **Best Common Type**
5. **Inference in Arrays**
6. **Inference in Objects**
7. **Type Inference with Generics**

---

# 1. **Basic Variable Inference**

## Overview:

When you declare a variable and assign a value, TypeScript automatically infers the type of that variable based on the value. This saves you from having to explicitly define the type.

## Example:

```typescript
let name = "Mahesh"; // TypeScript infers `name` as type `string`
let age = 30; // TypeScript infers `age` as type `number`
let isDeveloper = true; // TypeScript infers `isDeveloper` as type `boolean`
```

## Explanation:

- `name` is inferred to be a string because the initial value is a string.
- `age` is inferred to be a number.
- `isDeveloper` is inferred to be a boolean.

**Note:** Once inferred, the variable cannot be reassigned to a different type without causing an error.

```typescript
name = 42; // Error: Type 'number' is not assignable to type 'string'
```

---

# 2. **Function Return Type Inference**

## Overview:

When you declare a function without specifying the return type, TypeScript will infer the return type based on the function’s implementation.

## Example:

```typescript
function add(a: number, b: number) {
  return a + b; // TypeScript infers return type as `number`
}

const result = add(5, 10); // result is inferred as `number`
```

## Explanation:

- The function `add` returns the result of `a + b`. Since `a` and `b` are both numbers, TypeScript infers the return type of `add` as `number`.
- The variable `result` is automatically inferred as a number when it stores the return value of `add`.

---

# 3. **Contextual Typing**

## Overview:

Contextual typing occurs when TypeScript infers types based on the context in which the variable or function is used. This is common in event handlers, callback functions, and other situations where the type is inferred from the surrounding code.

## Example:

```typescript
const button = document.querySelector("button");

button?.addEventListener("click", (event) => {
  console.log(event.target); // TypeScript infers the type of `event` as `MouseEvent`
});
```

## Explanation:

- In the `addEventListener` function, TypeScript knows that the `click` event is associated with a `MouseEvent`, so it infers the type of `event` as `MouseEvent` without explicitly defining it.

---

# 4. **Best Common Type**

## Overview:

When working with an array of values of different types, TypeScript will infer the "best common type" by analyzing the array's values.

## Example:

```typescript
let values = [1, 2, null]; // TypeScript infers `values` as (number | null)[]
```

## Explanation:

- The array contains both `number` and `null` values, so TypeScript infers the type of the array as `(number | null)[]`. This means the array can hold numbers and nulls, but nothing else.

---

# 5. **Inference in Arrays**

## Overview:

When an array is declared, TypeScript infers its type based on the values provided within the array.

## Example:

```typescript
let fruits = ["apple", "banana", "orange"]; // TypeScript infers `fruits` as string[]
```

## Explanation:

- TypeScript infers the type of `fruits` as `string[]`, meaning it is an array of strings.

---

# 6. **Inference in Objects**

## Overview:

When working with objects, TypeScript can infer the type of the object’s properties based on their assigned values.

## Example:

```typescript
let user = {
  name: "Mahesh",
  age: 30,
  isAdmin: true,
}; // TypeScript infers `user` as { name: string; age: number; isAdmin: boolean }
```

## Explanation:

- TypeScript automatically infers that the `user` object has the following structure:
  ```typescript
  {
    name: string;
    age: number;
    isAdmin: boolean;
  }
  ```

**Reassignment with Incorrect Types:**

```typescript
user.age = "thirty"; // Error: Type 'string' is not assignable to type 'number'
```

---

# 7. **Type Inference with Generics**

## Overview:

In cases where generics are used, TypeScript can infer the type parameter based on the values passed to the function.

## Example:

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let numberIdentity = identity(42); // TypeScript infers `T` as `number`
let stringIdentity = identity("Hello"); // TypeScript infers `T` as `string`
```

## Explanation:

- In the `identity` function, TypeScript infers the type of `T` based on the argument passed.
- For `identity(42)`, `T` is inferred as `number`.
- For `identity("Hello")`, `T` is inferred as `string`.

---

# 8. **Advanced Type Inference with Conditional Types**

## Overview:

When conditional types are used, TypeScript can infer types based on certain conditions during runtime, allowing for more flexible type inference.

## Example:

```typescript
type MessageType<T> = T extends string ? "text" : "binary";

let message: MessageType<string>; // TypeScript infers `message` as `text`
let binaryMessage: MessageType<number>; // TypeScript infers `binaryMessage` as `binary`
```

## Explanation:

- TypeScript uses the conditional type `T extends string ? "text" : "binary"` to infer whether a `MessageType` should be `text` or `binary` based on the provided type.
- For `string`, TypeScript infers `MessageType<string>` as `"text"`.
- For `number`, TypeScript infers `MessageType<number>` as `"binary"`.

---

# Summary

- **Basic Variable Inference:** Automatically determines variable types based on values.
- **Function Return Type Inference:** Infers the return type of a function based on the return statement.
- **Contextual Typing:** Infers types from the context in which a variable or function is used.
- **Best Common Type:** Determines the most specific type when working with arrays of multiple types.
- **Inference in Arrays/Objects:** Infers the types of array and object properties based on values assigned.
- **Generics Inference:** Infers generic types based on function arguments.
- **Advanced Inference with Conditional Types:** Uses conditions to infer more complex types.

With this knowledge, you can write more concise and maintainable TypeScript code without sacrificing type safety!
