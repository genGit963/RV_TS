### TypeScript Class and Method Decorators: A Comprehensive Guide

#### Overview:

In TypeScript, decorators are `special types of declarations that can be attached to classes, methods, properties, or parameters`. They <u>provide a way to add metadata, modify behavior, or extend functionality without altering the actual code logic</u>. Understanding the decorator pattern and its use cases will allow you to harness the power of metaprogramming in TypeScript to create cleaner, more maintainable code.

#### **Table of Contents:**

1. Introduction to Decorators
   - What are Decorators?
   - Why Use Decorators?
   - Enabling Decorators in TypeScript
2. Understanding the Decorator Pattern
   - What is the Decorator Pattern?
   - Use Cases of the Decorator Pattern
3. Class Decorators
   - Implementing Class Decorators
   - Example: Logging Class Instantiation
4. Method Decorators
   - Implementing Method Decorators
   - Example: Logging Method Calls
   - Example: Method Authorization
5. Property Decorators
   - Implementing Property Decorators
   - Example: Default Value Property
6. Advanced Use Cases
   - Applying Multiple Decorators
   - Composable Decorators
   - Metadata Reflection with Decorators
7. Conclusion and Best Practices

---

### 1. **Introduction to Decorators**

#### What are Decorators?

Decorators are functions that take the target (class, method, property) as an argument and allow you to modify or enhance it. They are widely used in frameworks like Angular to handle things like dependency injection and routing.

#### Why Use Decorators?

- **Separation of Concerns**: Keep logic such as logging, validation, or authorization outside the main code logic.
- **Code Reusability**: Decorators allow you to write once, reuse everywhere.
- **Clean and Scalable Code**: They help in reducing code duplication by modularizing logic.

#### Enabling Decorators in TypeScript

To use decorators, you need to enable the feature in your `tsconfig.json`:

```json
{
  "experimentalDecorators": true,
  "emitDecoratorMetadata": true
}
```

---

### 2. **Understanding the Decorator Pattern**

#### What is the Decorator Pattern?

The decorator pattern is a structural design pattern that allows behavior to be added to individual objects, statically or dynamically, without affecting the behavior of other objects from the same class.

#### Use Cases of the Decorator Pattern:

- **Logging**: Automatically log when a method is called.
- **Validation**: Ensure certain conditions are met before a method executes.
- **Caching**: Cache the result of expensive method calls.

---

### 3. **Class Decorators**

#### Implementing Class Decorators:

A class decorator is a function that is applied to the constructor of the class. It can be used to modify or replace the class at runtime.

**Syntax**:

```ts
function classDecorator(target: Function) {
  // Modify or extend class behavior here
}
```

#### Example: Logging Class Instantiation

```ts
function LogClass(target: Function) {
  console.log(`Class ${target.name} is created.`);
}

@LogClass
class User {
  constructor(public name: string) {}
}

const user = new User("Mahesh");
// Output: Class User is created.
```

In this example, whenever the `User` class is instantiated, a log is printed.

---

### 4. **Method Decorators**

#### Implementing Method Decorators:

A method decorator takes three arguments: the class prototype, the method name, and the property descriptor. It allows you to modify the behavior of methods.

**Syntax**:

```ts
function methodDecorator(
  target: Object,
  propertyKey: string | symbol,
  descriptor: PropertyDescriptor
) {
  // Modify or extend method behavior here
}
```

#### Example 1: Logging Method Calls

```ts
function LogMethod(
  target: Object,
  propertyKey: string,
  descriptor: PropertyDescriptor
) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Method ${propertyKey} is called with args:`, args);
    return originalMethod.apply(this, args);
  };
}

class MathOperations {
  @LogMethod
  add(a: number, b: number) {
    return a + b;
  }
}

const math = new MathOperations();
math.add(5, 3);
// Output: Method add is called with args: [5, 3]
```

#### Example 2: Method Authorization

```ts
function RequiresRole(role: string) {
  return function (
    target: Object,
    propertyKey: string,
    descriptor: PropertyDescriptor
  ) {
    const originalMethod = descriptor.value;

    descriptor.value = function (...args: any[]) {
      if (this.role !== role) {
        throw new Error(
          `Unauthorized: ${this.role} role cannot execute ${propertyKey}`
        );
      }
      return originalMethod.apply(this, args);
    };
  };
}

class AdminOperations {
  role = "admin";

  @RequiresRole("admin")
  deleteUser(userId: string) {
    console.log(`User ${userId} deleted`);
  }
}

const admin = new AdminOperations();
admin.deleteUser("123");
// Output: User 123 deleted
```

---

### 5. **Property Decorators**

#### Implementing Property Decorators:

A property decorator can be used to modify or provide additional behavior when a property is set or retrieved.

**Syntax**:

```ts
function propertyDecorator(target: Object, propertyKey: string | symbol) {
  // Modify property behavior here
}
```

#### Example: Default Value Property

```ts
function DefaultValue(defaultValue: any) {
  return function (target: any, propertyKey: string) {
    let value = defaultValue;

    Object.defineProperty(target, propertyKey, {
      get: () => value,
      set: (newValue) => {
        value = newValue || defaultValue;
      },
      enumerable: true,
      configurable: true,
    });
  };
}

class UserSettings {
  @DefaultValue("light")
  theme!: string;
}

const settings = new UserSettings();
console.log(settings.theme); // Output: light
settings.theme = "dark";
console.log(settings.theme); // Output: dark
```

---

### 6. **Advanced Use Cases**

#### Applying Multiple Decorators:

Multiple decorators can be stacked on a single class or method by applying them one after another.

```ts
@LogClass
@AnotherDecorator
class MultiDecoratedClass {}
```

#### Composable Decorators:

Decorators can be composed by returning a new decorator from within a decorator function.

#### Metadata Reflection with Decorators:

TypeScript provides the `reflect-metadata` library to inspect metadata at runtime, enhancing the power of decorators.

---

### 7. **Conclusion and Best Practices**

- Use decorators to separate cross-cutting concerns (like logging and validation).
- Keep decorators simple and focused on one task.
- Avoid overusing decorators; they should enhance code, not obscure its intent.

By mastering decorators, you can write more modular, cleaner, and reusable code in TypeScript, making your codebase easier to maintain and extend.
