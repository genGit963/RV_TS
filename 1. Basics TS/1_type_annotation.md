### Overview: Type Annotations in TypeScript

TypeScript's type annotations provide a way to explicitly define types for variables, function parameters, and return values, offering increased code clarity and preventing errors. This guide covers the fundamentals to advanced use of type annotations, ensuring a strong understanding of primitive types, arrays, tuples, and enums.

### Table of Contents

1. **Introduction to Type Annotations**
   - What are type annotations?
   - Benefits of using type annotations
2. **Primitive Types**
   - Number
   - String
   - Boolean
   - Example with code
3. **Arrays**
   - Annotating arrays with a single type
   - Multi-dimensional arrays
   - Example with code
4. **Tuples**
   - Defining fixed-length arrays with specific types
   - Accessing and modifying tuple elements
   - Example with code
5. **Enums**
   - Defining and using enums
   - Numeric and string enums
   - Example with code
6. **Function Parameters and Return Types**
   - Explicitly typing function parameters
   - Typing function return values
   - Example with code
7. **Advanced Concepts**
   - Union and intersection types
   - Type aliases
   - Optional and default parameters in functions
   - Example with code

---

### 1. **Introduction to Type Annotations**

Type annotations allow developers to declare the type of a variable or function in TypeScript. This is useful for:

- **Clarity**: You can see at a glance what type is expected.
- **Error prevention**: TypeScript ensures that variables or functions only accept values of the correct type.

### 2. **Primitive Types**

TypeScript provides the following primitive types:

- `number`
- `string`
- `boolean`

**Example:**

```typescript
let age: number = 25; // Declaring a number
let name: string = "Mahesh"; // Declaring a string
let isActive: boolean = true; // Declaring a boolean

// Error: TypeScript will throw an error if the wrong type is assigned
age = "twenty"; // Error: 'string' is not assignable to 'number'
```

### 3. **Arrays**

In TypeScript, you can define the type of elements in an array.

- **Single Type Array**: Array with one type.
- **Multi-dimensional Arrays**: Arrays containing arrays of a certain type.

**Example:**

```typescript
let numbers: number[] = [1, 2, 3, 4]; // Array of numbers
let names: string[] = ["Mahesh", "James", "John"]; // Array of strings

// Multi-dimensional array (array of arrays)
let matrix: number[][] = [
  [1, 2],
  [3, 4],
];
```

### 4. **Tuples**

Tuples allow you to define an array with fixed-length and specific types at each index.

**Example:**

```typescript
let person: [string, number, boolean] = ["Mahesh", 25, true]; // A tuple with string, number, and boolean

// Accessing tuple elements
console.log(person[0]); // Outputs: "Mahesh"

// Modifying tuple values
person[1] = 30; // Changing the number
```

### 5. **Enums**

Enums allow you to define a set of named constants, which can be either numeric or string-based.

- **Numeric Enums**: By default, enums are numeric.
- **String Enums**: You can also define string enums.

**Example:**

```typescript
// Numeric enum
enum Role {
  Admin = 1,
  User = 2,
  Guest = 3,
}

let userRole: Role = Role.Admin;
console.log(userRole); // Outputs: 1

// String enum
enum Status {
  Active = "ACTIVE",
  Inactive = "INACTIVE",
  Pending = "PENDING",
}

let currentStatus: Status = Status.Active;
console.log(currentStatus); // Outputs: "ACTIVE"
```

### 6. **Function Parameters and Return Types**

You can specify the types of a function’s parameters and the type it returns. This ensures that the function is used correctly.

**Example:**

```typescript
// Function with typed parameters and return type
function add(a: number, b: number): number {
  return a + b;
}

console.log(add(5, 10)); // Outputs: 15
// Error: The following would throw an error because we're passing a string
// console.log(add(5, "10"));
```

### 7. **Advanced Concepts**

- **Union Types**: Allow a variable to accept multiple types.
- **Intersection Types**: Combine multiple types into one.
- **Type Aliases**: Define custom types for reusability.
- **Optional and Default Parameters**: Mark function parameters as optional or provide default values.

**Example:**

```typescript
// Union type (number or string)
let id: number | string;
id = 123; // OK
id = "ABC"; // Also OK

// Intersection type
type User = { name: string; age: number };
type Admin = { role: string };
type AdminUser = User & Admin;

let admin: AdminUser = {
  name: "Mahesh",
  age: 30,
  role: "Admin",
};

// Type alias
type Point = { x: number; y: number };
let point: Point = { x: 10, y: 20 };

// Optional parameter
function greet(name: string, greeting?: string) {
  if (greeting) {
    console.log(`${greeting}, ${name}`);
  } else {
    console.log(`Hello, ${name}`);
  }
}

greet("Mahesh"); // Outputs: Hello, Mahesh
greet("Mahesh", "Good morning"); // Outputs: Good morning, Mahesh
```

---

This structure guides you from basic types to advanced techniques, ensuring you understand how to effectively use TypeScript's type system.
