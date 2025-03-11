# ARTEA SPRINT1

**Assigner** : Kang Cecep

**Period** : 14 Feb 2025 - 28 Feb 2025

**Task** : Pelajari web app

## Timeline Breakdown

[Artea SPRINT1 Timeline Breakdown](https://www.notion.so/msultonet-changer/18f2b15f7adc817082faca7c032fcdd0?v=18f2b15f7adc81f3bd4b000ccbe8ced4&pvs=4)

## Learning Summary

### 1. Bahasa Pemrograman

- Javascript:
  - konsep fundamental (data types, control flow),
  - javascript functions,
  - ES6+,
  - Async Programming,
  - DOM manipulation & event handling,
- Typescript
  - Static typing
  - Interface, Type, Enum, Class
  - Complex types (unions, intersections, mapped types)
  - Classes, Object and OOP

### 2. Framework

- Client-side / frontend
  - vue
    - Vue templates directives
    - data binding (one way vs two way using v-bind and v-model)
    - Component-based architecture.
    - State management (Redux, Vuex, or Pinia).
    - Lifecycle methods and hooks (React) or reactivity system (Vue).
- Server-side / backend
  - express js
    - middleware (application level, router level)
    - routing fundamentals (get, post, put , delete)
    - RESTful API development.
    - Error handling and request validation.

### 3. Web App architecture

- Client-server communication using HTTP/HTTPS protocols.
- Single-page applications (SPA) vs. server-rendered applications.
- Integration with databases and external APIs.

### 4. Clean Code Principles

- Code readability and maintainability.
- SOLID principles for object-oriented design.
- DRY (Don't Repeat Yourself) and KISS (Keep It Simple, Stupid) principles.
- Proper naming conventions and modular code structure.

### 5. Project Structure

- ayered architecture (controllers, services, repositories, models).
- 3-Tier Architecture: Divides the application into Presentation, Logic, and
  Data layers, simplifying maintenance and scalability.
- Hexagonal Architecture (Ports and Adapters): Focuses on core business logic
  and isolates external systems for better testability.
- Example for Minimarket:
- Presentation Layer: React/Vue components for inventory and sales dashboards.
- Logic Layer: Express services for pricing and discount calculations.
- Data Layer: Repository classes interacting with a database of products,
  customers, and transactions.
- Organizing files based on features or domain (feature-based structure).

- Environment configuration and dependency management.

- For small applications like a minimarket app, consider using a domain-driven
  structure where each domain (e.g., products, customers, sales) has its own
  folder containing its models, services, and controllers.

### 6. Security and Optimization

- Authentication and authorization strategies (e.g., JWT, OAuth2).

- Input validation and sanitization to prevent attacks (e.g., SQL injection,
  XSS).

- Performance optimization through caching and database indexing.

## Learning Sheet Documentation

### 1. Bahasa Pemrograman

#### 1.1 Javascript

- Variables (var, let, const) dalam development banyak menggunakan const
- Data Types and coercien

  contoh dalam proses pemrosesan input:

  ```
  let age = "25";
  let nextYear = age + 1; // '251' due to concatenation
  let correctNextYear = Number(age) + 1; // 26
  ```

- Functions Expression, arrow function, closures digunakan untuk code
  reusability dan modularity

  contoh penggunaan arrow functions (bentuk sederhana functions):

  ```
  const add = (a, b) => a + b; // no bracket directly return
  console.log(add(5, 3)); // 8
  ```

  contoh penggunaan closures:

  ```
  function createCounter() {
    let count = 0;
    return function () {
      return ++count;
    };
  }
  const counter = createCounter();
  console.log(counter()); // 1
  console.log(counter()); // 2
  ```

- Control flow (Loops, conditionals, and Switch Statements) penggunaan if-else
  atau switch-case statements

- OOP pada javascript dengan prototype dan object
  ```
  class Car {
    constructor(brand, model) {
      this.brand = brand;
      this.model = model;
    }
    display() {
      return `${this.brand} ${this.model}`;
    }
  }
  const myCar = new Car("Toyota", "Corolla");
  console.log(myCar.display()); // Toyota Corolla
  ```
- ES6+ Features

  - Destructuring
    ```
    const user = { name: "Alice", age: 30, location: "New York" };
    const { name, age } = user;
    console.log(`${name} is ${age} years old.`); // Alice is 30 years old.
    ```
  - Template literals

    contoh penggunaan dalam membuat deskripsi product

    ```
    const product = "Laptop";
    const price = 1200;
    const description = `The product ${product} costs $${price}.`;
    console.log(description); // The product Laptop costs $1200.
    ```

    contoh multiline string

    ```
    const message = `Hello,
                    This is a multiline string
                    using template literals.
                    `;
    console.log(message);
    ```

  - Spread/rest operators dalam penggunaan arrays/objects

    contoh copying dan merging arrays

    ```
    const numbers = [1, 2, 3];
    const newNumbers = [...numbers, 4, 5];
    console.log(newNumbers); // [1, 2, 3, 4, 5]
    ```

    contoh merging objects

    ```
    const user1 = { name: "Alice", age: 25 };
    const user2 = { location: "NYC", profession: "Engineer" };
    const mergedUser = { ...user1, ...user2 };
    console.log(mergedUser);
    ```

    contoh penggunaan rest operatos sebagai function parameters

    ```
    function sum(...numbers) {
      return numbers.reduce((acc, num) => acc + num, 0);
    }
    console.log(sum(1, 2, 3, 4)); // 10
    ```

- Async Programming

  - Callbacks

    callback adalah sebuah function yang dimasukkan sebagai argument pada
    function lain yang biasa digunakan pada proses asynchronous

    ```
    function fetchData(callback) {
      setTimeout(() => {
        callback("Data received");
      }, 2000);
    }

    function displayData(data) {
      console.log(data);
    }

    fetchData(displayData); // Output after 2s: "Data received"
    ```

  - promises

    promises menyediakan fitur yang lebih praktis daripada callbacks agar
    menghindari "callback hells"

    Promise Terminology:

    - Pending: The initial state when the promise is neither fulfilled nor
      rejected.

    - Fulfilled: The operation was completed successfully, and .then() is
      executed.

    - Rejected: The operation failed, and .catch() is executed.

    - Settled: The promise is either fulfilled or rejected but no longer
      pending.

    ```
    function fetchProduct(productId) {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          if (productId) {
            resolve({ id: productId, name: "Laptop" });
          } else {
            reject("Product not found");
          }
        }, 2000);
      });
    }

    fetchProduct(101)
      .then(product => console.log("Product found:", product))
      .catch(error => console.log("Error:", error));
    ```

  - async/await

    contoh async ketika melakukan fetching data API

    ```
    async function fetchProduct(productId) {
      let response = await fetch(`https://api.example.com/products/${productId}`);
      let data = await response.json();
      console.log(data);
    }
    fetchProduct(101);
    ```

  - Perbedaan antara callbacks, promises, async/await dan kapan ketika
    menggunakan ketiganya

    | Method    | Pros                                                         | Cons                                      | When to use                                                                                      |
    | --------- | ------------------------------------------------------------ | ----------------------------------------- | ------------------------------------------------------------------------------------------------ |
    | Callbacks | Simple for small tasks, works well in event-driven scenarios | Leads to "callback hell" if nested deeply | When handling simple asynchronous tasks like event listeners or reading files                    |
    | Promises  | Cleaner syntax, avoids callback hell                         | Still requires chaining with .then()      | When handling multiple async operations that depend on each other                                |
    | Async     | More readable, looks like synchronous code                   | Requires try/catch for error handling     | When dealing with complex asynchronous operations that need to be written in a synchronous style |

- DOM manipulation and event handling

  core concepts:

  - Selecting elements `(document.querySelector, document.getElementById)`
  - modifying elements `(element.textContent, element.style)`
  - handling events `(addEventListener)`

#### 1.2 Typescript

- **Static Typing:**

  - TypeScript enforces type checking at compile time, reducing runtime errors.
  - Example:
    ```ts
    let username: string = "JohnDoe";
    let age: number = 30;
    ```

- **Interface, Type, Enum, Class:**

  - **Interface:** Defines the shape of an object.

    Scenario: Defining a data structure for an API response

    - Use Case: When you need to ensure a consistent shape for objects,
      especially when working with external data such as APIs.

    - Example: Imagine you're fetching user data from an API, and you want to
      enforce the structure of the response.

    Why use Interface?

    - Supports declaration merging (easier to extend later).
    - Works well with object-oriented structures.
    - More readable for defining API responses or database models.

    ```ts
    interface User {
      id: number;
      name: string;
    }
    let user: User = { id: 1, name: "Alice" };
    ```

  - **Type:** Similar to interfaces but allows unions and intersections.

    Scenario: Creating reusable and complex type combinations

    - Use Case: When defining union types, mapped types, or primitive aliases
      that do not require extension.

    - Example: Defining different types of valid user roles in an application.

    Why use Type?

    - More flexible than interfaces for unions (| operator).
    - Ideal for defining primitive-based types (e.g., string, number).
    - Cannot be extended like interfaces (useful for fixed definitions).

    ```ts
    type Status = "active" | "inactive";
    let userStatus: Status = "active";
    ```

  - **Enum:** A set of named constants.

    Scenario: Defining fixed, named constants

    - Use Case: When you need a fixed set of named values that will be used in
      different parts of the application.

    - Example: Defining HTTP response statuses in an API.

    Why use Enum?

    - Prevents magic numbers (instead of using 200, 404, etc.).
    - Better readability in switch statements or logic flows.
    - Avoids errors when dealing with fixed, well-known categories.

    ```ts
    enum HttpStatus {
      OK = 200,
      BAD_REQUEST = 400,
      UNAUTHORIZED = 401,
      NOT_FOUND = 404
    }

    const getResponseMessage = (status: HttpStatus) => {
      switch (status) {
        case HttpStatus.OK:
          return "Success";
        case HttpStatus.BAD_REQUEST:
          return "Bad Request";
        case HttpStatus.UNAUTHORIZED:
          return "Unauthorized";
        case HttpStatus.NOT_FOUND:
          return "Not Found";
        default:
          return "Unknown Status";
      }
    };

    console.log(getResponseMessage(HttpStatus.OK)); // Output: "Success"
    ```

  - **Class:** Encapsulates data and behavior in OOP.

    Scenario: Creating objects with methods and behavior

    - Use Case: When you need to define both data and behavior together.

    - Example: A Car class that defines properties and behaviors.

    Why use Class?

    - Used for object-oriented programming (OOP).
    - Supports encapsulation (private properties).
    - Can have methods and inheritance, unlike types and interfaces.

    ```ts
    class Person {
      name: string;
      constructor(name: string) {
        this.name = name;
      }
      greet() {
        return `Hello, ${this.name}`;
      }
    }
    let person = new Person("John");
    console.log(person.greet());
    ```

- **Complex Types (Unions, Intersections, Mapped Types):**

  - **Union Type:** A variable can hold multiple types.
    ```ts
    type ID = number | string;
    let userId: ID = "123";
    ```
  - **Intersection Type:** Combines multiple types.
    ```ts
    interface Employee {
      name: string;
    }
    interface Manager {
      department: string;
    }
    type Lead = Employee & Manager;
    let teamLead: Lead = { name: "Alice", department: "IT" };
    ```
  - **Mapped Types:** Used to transform object properties.
    ```ts
    type Optional<T> = {
      [P in keyof T]?: T[P];
    };
    interface User {
      id: number;
      name: string;
    }
    type PartialUser = Optional<User>;
    ```

- **Classes, Object, and OOP:**

  - **Encapsulation:** Data is hidden and accessed through methods.
  - **Inheritance:** A child class inherits from a parent class.
    ```ts
    class Animal {
      constructor(public name: string) {}
      makeSound() {
        console.log("Some generic sound");
      }
    }
    class Dog extends Animal {
      makeSound() {
        console.log("Bark");
      }
    }
    let myDog = new Dog("Buddy");
    myDog.makeSound(); // Bark
    ```
  - **Polymorphism:** Methods behave differently in different contexts.
  - **Abstraction:** Hides implementation details from the user

  | Feature                       | Interface                   | Type Alias                  | Enum   | Class                    |
  | ----------------------------- | --------------------------- | --------------------------- | ------ | ------------------------ |
  | **Extensible**                | ✅ Yes (can extend & merge) | ❌ No                       | ❌ No  | ✅ Yes (via inheritance) |
  | **Can have methods?**         | ❌ No                       | ❌ No                       | ❌ No  | ✅ Yes                   |
  | **Best for object shape?**    | ✅ Yes                      | ✅ Yes (but not extendable) | ❌ No  | ✅ Yes                   |
  | **Best for primitive types?** | ❌ No                       | ✅ Yes                      | ❌ No  | ❌ No                    |
  | **Best for constants?**       | ❌ No                       | ❌ No                       | ✅ Yes | ❌ No                    |

- **Summary**
  - Use interface when defining the structure of objects, especially API
    responses or models.
  - Use type for defining unions, complex types, or primitive-based types.
  - Use enum when you need a fixed list of named constants.
  - Use class when you need a blueprint with data + behavior (methods),
    following OOP principles.

### 2. Frameworks

#### Client-side / Frontend

##### Vue.js

- **Vue Templates and Directives:**

  - Vue uses a declarative template syntax to bind the DOM to Vue instance data.
  - Example:

    ```
    <template>
      <h1>{{ message }}</h1>
    </template>
    <script>
    export default {
      data() {
        return {
          message: "Hello Vue!"
        };
      }
    };
    </script>
    ```

  - Vue 3 Directives Cheat Sheet

| Directive                           | Description                                                                          | Example                                                                                                                                                                                                              |
| ----------------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **v-text**                          | Updates the text content of an element.                                              | `<h1 v-text="title"></h1>`<br>Equivalent to: `<h1>{{ title }}</h1>`                                                                                                                                                  |
| **v-html**                          | Renders HTML content within an element. **Use with caution to prevent XSS attacks.** | `<div v-html="rawHtml"></div>`<br>If `rawHtml = '<p>Sample</p>'`, it renders as: `<div><p>Sample</p></div>`                                                                                                          |
| **v-show**                          | Toggles the element's visibility based on a boolean value.                           | `<p v-show="isVisible">Hello</p>`<br>If `isVisible` is `false`, the paragraph is hidden (CSS `display: none`).                                                                                                       |
| **v-if**                            | Conditionally renders the element based on the expression's truthiness.              | `<p v-if="isLoggedIn">Welcome back!</p>`<br>Renders only if `isLoggedIn` is `true`.                                                                                                                                  |
| **v-else-if**                       | Denotes the "else if" block for `v-if`.                                              | `<p v-if="score >= 90">A</p><p v-else-if="score >= 80">B</p><p v-else>Below B</p>`                                                                                                                                   |
| **v-else**                          | Denotes the "else" block for `v-if`.                                                 | See `v-else-if` example above.                                                                                                                                                                                       |
| **v-for**                           | Renders a list of items by iterating over an array or object.                        | `<li v-for="item in items" :key="item.id">{{ item.name }}</li>`<br>Loops through `items` and renders each item's name.                                                                                               |
| **v-on**                            | Attaches event listeners to elements.                                                | `<button v-on:click="submitForm">Submit</button>`<br>Shorthand: `<button @click="submitForm">Submit</button>`                                                                                                        |
| **v-bind**                          | Dynamically binds one or more attributes, or a component prop, to an expression.     | `<img v-bind:src="imageSrc" alt="Image">`<br>Shorthand: `<img :src="imageSrc" alt="Image">`                                                                                                                          |
| **v-model**                         | Creates a two-way binding on form input, textarea, and select elements.              | `<input v-model="username" placeholder="Enter your name">`<br>`username` is updated as the user types.                                                                                                               |
| **v-slot**                          | Denotes named slots in a child component.                                            | `<template v-slot:header>Header Content</template>`<br>Used within a component to inject content into a named slot.                                                                                                  |
| **v-pre**                           | Skips compilation for this element and all its children.                             | `<span v-pre>{{ raw }}</span>`<br>Renders as `{{ raw }}` without compiling.                                                                                                                                          |
| **v-once**                          | Renders the element and component once only, and skips future updates.               | `<p v-once>{{ message }}</p>`<br>`message` will not update if its data changes.                                                                                                                                      |
| **v-memo**                          | Memoizes a sub-tree of the template to optimize rendering.                           | `<div v-memo="[value]">...</div>`<br>Re-renders only if `value` changes.                                                                                                                                             |
| **v-cloak**                         | Keeps the element cloaked until the Vue instance finishes compiling.                 | `<div v-cloak>{{ message }}</div>`<br>Useful to prevent flash of uncompiled content.                                                                                                                                 |
| **Custom Directive**                | User-defined directive to encapsulate reusable DOM manipulations.                    | `javascript<br>app.directive('focus', { mounted(el) { el.focus(); }});<br>`<br>Usage: `<input v-focus>` Focuses input on mount.                                                                                      |
| **Custom Directive with Modifiers** | Custom directive that reacts to modifiers for enhanced behavior.                     | `javascript<br>app.directive('format', { mounted(el, binding) { if (binding.modifiers.uppercase) { el.style.textTransform = 'uppercase'; }}});<br>`<br>Usage: `<p v-format.uppercase>Text</p>` Makes text uppercase. |

- Create Custom Directives

  - Directive lifecycle hooks

  | Hook          | Description                                         |
  | ------------- | --------------------------------------------------- |
  | created       | Called once when the directive is attached.         |
  | beforeMount   | Called before the element is inserted into the DOM. |
  | mounted       | Called when the element is inserted into the DOM.   |
  | beforeUpdate  | Called before the element is updated.               |
  | updated       | Called after the element is updated.                |
  | beforeUnmount | Called before the element is removed from the DOM.  |
  | unmounted     | Called after the element is removed from the DOM.   |

- **Data Binding (One-Way vs Two-Way using v-bind and v-model):**

  - One-way binding (`v-bind`):
    ```vue
    <img v-bind:src="imageUrl" />
    ```
  - Two-way binding (`v-model`):
    ```vue
    <input v-model="username" />
    ```

- **Component-Based Architecture:**

  - Vue applications are composed of reusable components.
  - Example:
    ```vue
    <template>
      <button @click="increment">Clicked {{ count }} times</button>
    </template>
    <script>
    export default {
      data() {
        return {
          count: 0
        };
      },
      methods: {
        increment() {
          this.count++;
        }
      }
    };
    </script>
    ```

- **State Management (Redux, Vuex, or Pinia):**

  - Vuex (Centralized State Management):
    ```js
    import { createStore } from "vuex";
    const store = createStore({
      state() {
        return { count: 0 };
      },
      mutations: {
        increment(state) {
          state.count++;
        }
      }
    });
    ```
  - Pinia (Modern lightweight alternative to Vuex):
    ```js
    import { defineStore } from "pinia";
    export const useCounterStore = defineStore("counter", {
      state: () => ({ count: 0 }),
      actions: {
        increment() {
          this.count++;
        }
      }
    });
    ```

- **Lifecycle Methods and Reactivity System:**
  - Lifecycle methods (e.g., `mounted`, `created`) allow execution of code at
    different stages of a component’s lifecycle.
    ```vue
    <script>
    export default {
      created() {
        console.log("Component is created");
      }
    };
    </script>
    ```
  - Vue 3 Reactivity System:
    ```js
    import { reactive } from "vue";
    const state = reactive({ count: 0 });
    function increment() {
      state.count++;
    }
    ```

**End Goal:** The learner will be able to build scalable, maintainable, and
secure web applications by applying best practices in TypeScript/JavaScript,
utilizing modern frameworks like React/Vue, and following clean code principles
with server-side boilerplates.
