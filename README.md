# 🎭 Interface vs Type in TypeScript: Understanding the Key Differences

> Imagine you’re directing a movie called **“Shape of Data.”**  
> The two main roles?  
> **Interface** and **Type.**  
> Now you, as the developer-director, must decide who plays the lead.

Before that, let's get introduced to the two heroes of our movie.

## 👮 Interface: The Structured Specialist

Interfaces are designed to define the shape of objects. If your goal is to describe a structure or contract (for classes or plain objects), `interface` is often the best choice.

```ts
interface User {
  name: string;
  age: number;
}
```
One significant benefit of interfaces is **declaration merging**, which allows extending the same interface across multiple declarations.

```ts
interface User {
  email: string;
}
// Now User has: name, age, and email
```
This makes interfaces ideal for working with public APIs or extending third-party types.

## 🧪 Type: The Flexible Typist

The `type` in TypeScript is all about flexibility and advanced type modeling. It allows you to:

- Define unions and intersections

- Compose complex types

- Represent primitives, tuples, and more

```ts
// Type Alias: Just giving a name to a type
type Status = "active" | "inactive"; // union of string literals

// Type Alias: Defining basic user info
type BasicInfo = {
  name: string;
  age: number;
};

// Type Alias: Defining contact info
type ContactInfo = {
  email: string;
  phone?: string; // optional
};

// Union Type: A user can be either a normal user or an admin
type Role = "user" | "admin"; // union type

// Intersection Type: Combining multiple types into one
type User = BasicInfo & ContactInfo & {
  role: Role;
  status: Status;
};

// Now use the User type
const user1: User = {
  name: "Amy",
  age: 22,
  email: "amy@example.com",
  role: "admin",
  status: "active"
  // phone is optional
};

```
Unlike `interface`, the `type` keyword in TypeScript offers more flexibility, especially when working with non-object types such as primitives, unions, intersections, or tuples.

## ⚖️ Interface vs Type: Quick Comparison

### 🔹 1. Interface:

- Used to define the shape of an object (structure).

- Works naturally with `class`, ideal for object-oriented programming (OOP).

- Supports declaration merging, multiple interfaces with the same name combine automatically.

- Can be extended using the `extends` keyword.

- Best suited for public APIs or when building reusable object contracts.

- Limited when it comes to defining unions, primitives, or tuples.

### 🔹 2. Type:

- Can define not only object shapes, but also unions, intersections, primitives, tuples, and more.

- Great for composing complex types or combining multiple types into one.

- Does not support declaration merging.

- Uses `&` (intersection) and `|` (union) for combining types.

- Offers more flexibility than `interface` in many advanced type scenarios.

- Can be used with classes, but feels less intuitive than `interface`.

## When Should You Use What?

### Use `interface` when:

- We're defining the structure of an object.

- We're working with class-based systems.

- We need to extend or merge types across files/modules.

### Use `type` when:

- We need to create unions, intersections, or complex compositions.

- We're working with non-object types like tuples, string literals, or functions.

- We need more advanced or flexible type modeling.

## 🎬 Final Scene: Whom to Choose, Whom to Let Go?

Inspector `Interface` and Technician `Type` — both are essential.
They’re not competitors — they’re collaborators.
Understand your task, and cast the right character in the right role.


---


# 📌 Understanding `Union (|)` vs `Intersection (&)` Types in TypeScript

In TypeScript, we often need to work with multiple types. That's where Union (`|`) and Intersection (`&`) types come in.

### 🔸 Union Type (`|`)
A Union Type means a value can be of either one type or another, but not necessarily both.
```ts
// Union: Either one of the types
type AorB = A | B;
```

### 🔸 Intersection Type (`&`)
An Intersection Type means a value must satisfy all the types, in other words, it must have all the properties of both types.
```ts
// Intersection: Must satisfy both types
type AandB = A & B;
```


### 🔹 Real-World Example: Admin vs User vs SuperAdmin
Let’s break this down with a practical example:

```ts
type Admin = {
    username: string;
    role: 'admin';
    permissions: string[];
};
  
type RegularUser = {
    username: string;
    role: 'user';
    email: string;
};
```
Now, we define a type that can be either an Admin or a RegularUser using **Union**:
```ts
type User = Admin | RegularUser;
```
And here's a function to display the dashboard based on the user's role:
```ts
function showDashboard(user: User) {
    console.log(`Welcome, ${user.username}`);
    if (user.role === 'admin') {
      console.log(`Permissions: ${user.permissions.join(', ')}`);
    } else {
      console.log(`Email: ${user.email}`);
    }
}
```
TypeScript uses type narrowing based on the `role` to safely access the relevant properties.

### 🔸 SuperAdmin: Using Intersection Type
Let’s now define a `SuperAdmin` who has everything from the `Admin` type plus extra fields — using 
Intersection:
```ts
type SuperAdmin = Admin & {
    email: string;
    superPower: true;
};

const root: SuperAdmin = {
    username: 'root',
    role: 'admin',
    permissions: ['ALL'],
    email: 'root@system.com',
    superPower: true,
};
```
Here, `SuperAdmin` combines all properties from `Admin` and adds `email` and `superPower`.

### ✅ Summary
| Type                   | Meaning                                        |
| ---------------------- | ---------------------------------------------- |
| `A \| B` (Union)       | Value can be either type A or type B           |
| `A & B` (Intersection) | Value must have all properties of both A and B |

Union types help create flexible APIs, while intersection types are great for extending types with additional functionality.
  
  



