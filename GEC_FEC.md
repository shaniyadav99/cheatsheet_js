# JavaScript Execution Contexts and Call Stack Cheat Sheet

## 1. JavaScript Execution Context (GEC & FEC)
- **Execution Context**: Defines the environment in which JavaScript code is executed.
- **Types**:
  - **Global Execution Context (GEC)**:
    - Default context for non-function code.
    - Contains global objects (`window` in browsers) and global `this`.
    - Example:  
      ```js
      var name = "John";
      function sayHello() {
          console.log("Hello, " + name);
      }
      sayHello(); // Output: Hello, John
      ```
  - **Function Execution Context (FEC)**:
    - Created when a function is called.
    - Contains local variables, arguments, and a reference to outer scopes via the **scope chain**.
    - Example:
      ```js
      function greet(name) {
          var message = "Hello, " + name;
          console.log(message);
      }
      greet("Alice"); // Output: Hello, Alice
      ```

## 2. Call Stack
- **Call Stack**: A LIFO (Last In, First Out) structure that tracks function calls.
- **Process**:
  1. When a function is invoked, its execution context is pushed onto the stack.
  2. When a function finishes execution, it is popped off the stack.
  - Example:
    ```js
    function first() { console.log("First"); second(); }
    function second() { console.log("Second"); third(); }
    function third() { console.log("Third"); }
    first(); // Output: First, Second, Third
    ```

## 3. Variable Environment
- **Global vs Local Variables**:
  - Global variables are accessible everywhere.
  - Local variables are confined to the function scope.
  - Example:
    ```js
    var globalVar = "Global";
    function display() {
        var localVar = "Local";
        console.log(globalVar);  // Output: Global
        console.log(localVar);   // Output: Local
    }
    display();
    // console.log(localVar);  // Error: localVar is not defined
    ```

## 4. Hoisting
- **Hoisting**: JavaScript moves variable and function declarations to the top of their scope during the memory creation phase.
  - **Function Hoisting**:
    - Entire function declarations are hoisted, allowing them to be called before definition.
    - Example:
      ```js
      sayHello();  // Output: Hello, world!
      function sayHello() {
          console.log("Hello, world!");
      }
      ```
  - **Variable Hoisting (with `var`)**:
    - Declarations are hoisted, but the initialization remains where it is.
    - Example:
      ```js
      console.log(a);  // Output: undefined
      var a = 10;
      console.log(a);  // Output: 10
      ```
  - **`let` and `const` Hoisting**:
    - Declarations are hoisted but not initialized, causing a **Temporal Dead Zone (TDZ)**.
    - Example:
      ```js
      console.log(b);  // ReferenceError
      let b = 20;
      ```

## 5. Scope Chain
- **Scope Chain**: Resolves variables by looking in the current execution context and moving up to outer contexts.
  - Example:
    ```js
    var name = "Global";
    function outer() {
        var name = "Outer";
        function inner() {
            var name = "Inner";
            console.log(name);  // Output: Inner
        }
        inner();
    }
    outer();
    ```

## 6. Recursion and Stack Overflow
- **Recursion**: A function calls itself to solve a problem.
  - Example:
    ```js
    function countdown(number) {
        if (number <= 0) {
            console.log("Done!");
            return;
        }
        console.log(number);
        countdown(number - 1);
    }
    countdown(5); // Output: 5, 4, 3, 2, 1, Done!
    ```
- **Stack Overflow**: Occurs if recursion doesn't have a base case, causing infinite calls and exceeding the call stack limit.
  - Example of infinite recursion (leads to stack overflow):
    ```js
    function infinite() {
        infinite();  // Infinite call - stack overflow
    }
    infinite();
    ```

---

## Key Takeaways:
- **GEC**: Created at script start, contains global variables and functions.
- **FEC**: Created on function invocation, contains local variables.
- **Call Stack**: Manages function calls in a LIFO order.
- **Hoisting**: Moves function and variable declarations to the top of their scope.
- **Scope Chain**: Resolves variables by searching from local to outer scopes.
- **Recursion**: Ensure a base case to prevent stack overflow.

