# Attributes and Methods

In this article, we'll be diving deep into **Attributes and Methods**, and as a practice exercise, we will be implementing a **BankAccount** class for better understanding.

## Attributes and Methods

### Attributes

Attributes (also called **properties** or **fields**) are the data or characteristics of an object. They represent the state of the object at any given moment.

Attributes are typically defined within a class and can hold different types of information related to the object.

For example, we wish to create two data fields for our `BankAccount` class:

- **Name:** To store the name of the account holder. The `string` data type would be best suited for it.
- **Balance:** To store the account balance. The `double` data type would be the perfect fit for this.

Since the attribute `balance` is personal information of the account holder, in a real-world scenario, this information should be hidden from the outside world. No user should be able to directly check the account balance of a different user.

To handle such cases, the **`balance`** attribute must be declared with the access modifier set to **`private`**.

### Methods

Methods are functions that are defined inside a class and represent the **behavior** or **actions** that an object of the class can perform.

Methods define what an object can do, and they often operate on the attributes (or fields) of the class. Every object of a class can call its methods to perform specific tasks.

For example, in a `BankAccount` class, different functions can be provided to the user:

- **Check Balance:** The user can check the account balance.
- **Deposit:** The user can deposit a certain amount.
- **Withdraw:** The user can withdraw money from their bank account.

Consider the following class implementing a `BankAccount` in the real world:

### C++

```cpp
#include <bits/stdc++.h>
using namespace std;

class BankAccount {
private:
    string name;
    double balance;

public:
    BankAccount(string name, double balance) {
        this->name = name;
        this->balance = balance;
    }

    void setName(string name) {
        this->name = name;
    }

    string getName() {
        return name;
    }

    double getBalance() {
        return balance;
    }

    void deposit(double amount) {
        balance += amount;
    }

    bool withdrawal(double amount) {
        if (amount > balance) {
            cout << "Insufficient amount" << endl;
            return false;
        }

        balance -= amount;
        return true;
    }
};
```

---

## Understanding the Interaction Between Attributes and Methods

In a class implementing a real-world scenario, the **attributes** and **methods** interact with each other constantly.

Methods allow controlled access to the attributes. In many cases, attributes are marked as `private` to restrict direct access from outside the class, promoting **encapsulation**.

Methods then provide a controlled way of interacting with those attributes.

For example, the `balance` attribute was set as `private` in the **BankAccount** class.

Now, in order to get the balance, there must be a method implemented that can access the private attribute.

This brings the two major methods used in real-world OOP projects:

- **Setters:** A method to set or modify the value of a particular attribute, such as `setName()`.
- **Getters:** A method to get or retrieve the value of a particular attribute, such as `getName()`.

These methods provide controlled access to private data attributes, which otherwise cannot be accessed directly from outside the class.

---

## Important Points

There are some important points that must be taken care of while implementing real-world entities using **Object-Oriented Programming**:

- **Accessing Attributes:** Use methods (getters and setters) to access private attributes to ensure controlled modification of data.

  **Example:**

  ```cpp
  getBalance();
  ```

  `getBalance()` retrieves the current balance.

- **Encapsulation:** Keep attributes private and provide controlled access using public methods to ensure data integrity.

  In C++, the `private` keyword strictly restricts outside access.

- **Default Values:** Attribute initialization rules depend on the language. In C++, member variables may contain indeterminate values if not initialized explicitly.

- **Method Parameters:** Methods can take parameters to modify attributes.

  **Example:**

  ```cpp
  deposit(amount);
  ```

- **Error Handling:** Always validate inputs inside methods, such as disallowing negative deposits or withdrawals exceeding the available balance.
