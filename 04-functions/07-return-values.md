## Return Values

---

```solidity
contract Functions7 {
  string name = 'Example 7';

  function getName1() public view returns(string memory) {
    return name;
  }

  function getName2() public view returns(string memory) {
    name;
  }
}
```

- `getName1` explicity returns the value of `name` `state variable`.
- The return **type** is `string memory`, and it works as expected, returning **"Example 7"**.
- `getName2` will not **compile** successfully because the **Solidity compiler** enforces that all functions with a `returns` declaration must include a corresponding `return` statement.
- In other words, the `returns` in the `function signature` serves as a **contract** or **promise** to the compiler that the function **will** return a value of the specified type.

---

#### Return function directly

```solidity
contract Functions7 {
  string name = 'Example 7';

  function getName1() public view returns(string memory) {
    return name;
  }

  function getName2() public view returns(string memory) {
    return getName1();
  }
}
```

- You can `return` the function directly without having to store it inside a variable first.
- As you can see here `getName2` in the **function expression** is returning `getName1()`.
- You do need to use the `()` right after the function name to call it properly.
- Without the `()`, **Solidity** will treat it as a function **pointer** or **reference** in memory.

---

#### Declaring the name in the function signature

```solidity
contract Functions7 {
  string name = 'Example 7';

  function getName1() public view returns(string memory) {
    return name;
  }

  function getName2() public view returns(string memory) {
    return getName1();
  }

  function getName3() public view returns(string memory anotherName) {
    anotherName = 'Another name';
  }
}
```

- **Solidity** knows to look for the value of `anotherName` and will return the value automatically without the keyword `return` in the function expression.
- This behaves similar to a `function parameter`, but it is not one because it is not being passed into the function.
- It is only used within the function for returning a value.

---

#### Returning multiple values

```solidity
contract Functions7 {
  string name = 'Example 7';

  function getName1() public view returns(string memory) {
    return name;
  }

  function getName2() public view returns(string memory) {
    return getName1();
  }

  function getName3() public view returns(string memory name1, string memory name2) {
    return (name, 'New name');
  }
}
```

- You must use the `return` keyword in the **function expression** when explicitly returning values.
- When returning multiple values, they need to be wrapped in `()` as a `tuple`.
- The first value in the `tuple`, `name`, refers to the `state variable`.
- The second value in the `tuple`, `"New name"`, is assigned to the `name2` return variable at **runtime**.
- Think of `name1` & `name2` as placeholders.

---

#### Return values from outside the smart contract

Values returned from a transaction are not available from outside of **EVM**.
This requires `events`.

```solidity
contract Functions7 {
  string name = 'Example 7';

  event NameChanged(string name);

  function setName1() public returns(string memory) {
    name = 'New name';
    emit NameChanged(name)  // Emit the event
    return name;            // Return the value (accessible only to the caller)
  }
}
```

- Creating an `Event`: You must define an `event`, such as `NameChanged`, and then `emit` it inside the function body whenever a significant action occurs (like updating name).
- Observability: `Events` allow data to be observed by external systems (e.g., frontend applications) by broadcasting it to the blockchain.
- Limitations of Return Values: Function return values are only available to the `contract` or transaction caller. They are not visible to external observers, which is why `events` are necessary.
