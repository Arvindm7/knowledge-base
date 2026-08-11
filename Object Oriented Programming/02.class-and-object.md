## Class

In object-oriented programming, a **Class** is a **blueprint** or **template** for creating objects. It is the logical representation that defines a set of attributes (data) and methods (functions) that the objects created from the class will have.

A class does not occupy memory on its own. It's essentially a definition or a structure from which individual objects are instantiated.

For example, consider the following code snippet representing an **Employee** class:

### Java

```java
import java.util.*;

class Employee {
    private int salary; // to store the salary of employee

    public String employeeName; // to store the name of employee

    // Method to set the employee name as given input
    public void setName(String s) {
        employeeName = s;
    }

    // Method to set the salary as given input
    public void setSalary(int val) {
        salary = val;
    }

    // Method to get the salary of the employee
    public int getSalary() {
        return salary;
    }
}
```

### Key Points

- The **Employee** class acts as a blueprint that has a set of attributes and methods defined in it, providing a logical meaning to a real-world entity, employee.
- The **Employee** class has a set of attributes (`employeeName` and `salary`) and a set of methods (functions like `setName()`, `setSalary()`, and `getSalary()`) providing different functionality.

---

## Object

An **object** is an instance of a class. When an object is created from a class, memory is allocated for it, and it holds the data as specified by the class.

An object interacts with other parts of the program, and methods can be called and attributes accessed that belong to it.

For example, consider the following code snippet demonstrating the creation of objects from the `Employee` class:

### Java

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Employee obj1 = new Employee();

        obj1.setName("Raj");
        obj1.setSalary(10000);

        Employee obj2 = new Employee();

        obj2.setName("Rahul");
        obj2.setSalary(15000);

        System.out.println("Salary of " + obj1.employeeName + " is " + obj1.getSalary());
        System.out.println("Salary of " + obj2.employeeName + " is " + obj2.getSalary());
    }
}
```

### Output

```text
Salary of Raj is 10000
Salary of Rahul is 15000
```

### Key Points

- The class by itself doesn't take any memory. It is the object that takes up memory once initialized.
- The two objects (`obj1` and `obj2`) have separate memory allocated for them even though they have the same attributes and methods.
- Each object maintains its own state.
- The code creates two separate objects (instances) of the **Employee** class, representing Raj and Rahul.

---

## Attributes & Behaviors

### Attributes

Attributes (also called **properties** or **fields**) are the data or characteristics of an object. They represent the **state** of the object at any given moment.

For example, in the **Employee** class, there are two attributes:

- `employeeName`
- `salary`

### Behaviors

Behaviors (also called **methods** or **functions**) are the actions or operations that an object can perform.

For example, in the **Employee** class, there are three behaviors/methods:

- `setName()`
- `setSalary()`
- `getSalary()`

---

## Creation of an Object

Objects are created from a class to access its attributes and behaviors.

**In Java**, objects are created using the `new` keyword, and variables store references to them.

### Java

```java
Employee obj1 = new Employee(); // reference → heap object
```

Here:

- `obj1` is a **reference variable**.
- `new Employee()` creates an **Employee object**.
- The object is allocated in the **heap**.
- `obj1` stores a reference to that object.

---

## Deletion of an Object

Object destruction and memory cleanup depend on the language's memory management model.

**In Java**, objects are automatically cleaned up by the **Garbage Collector (GC)** when no references remain to the object.

### Java

```java
Employee obj1 = new Employee();

obj1 = null; // object becomes eligible for GC
// Garbage Collector deletes it automatically
```

After `obj1 = null`, if there are no other references pointing to the object, it becomes **eligible for garbage collection**.

> **Note:** The Garbage Collector does not necessarily delete the object immediately. It decides when the memory should actually be reclaimed.

---

## Stack and Heap Memory Allocation

Different languages manage stack and heap memory differently.

In Java:

- Primitive local variables and object reference variables are typically stored in **stack frames**.
- All objects created using **`new`** are stored in the **heap**.
- Stack memory is automatically released when a method finishes execution.
- Heap memory is managed automatically by the **Garbage Collector**.

For example:

### Java

```java
Employee obj1 = new Employee();
```

Conceptually:

```text
Stack                         Heap
+-----------+                 +------------------+
| obj1      | --------------> | Employee object  |
+-----------+                 +------------------+
   reference                       object
```

Here, `obj1` is a reference variable stored in the stack frame, while the `Employee` object created using `new` is stored in the heap.
