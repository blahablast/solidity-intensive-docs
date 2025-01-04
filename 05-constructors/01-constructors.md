## Constructors

---

A special function that runs once and only once whenever a `smart contract` is put on the blockchain.
`Constructors` are typically used to `initialize` the `contract's` **state** or define behaviors that need to be set up during deployment.

---

#### How to use a Constructor (or not use)

```solidity
contract Constructors1 {
  string public name = 'Example 1';
}
```

Constructors are **not** required in a `smart contract`. As you can see from the above example.

```solidity
contract Constructor2 {
  string public name;

  constructor() {
    name = 'Example 2';
  }
}
```

- It is just named `constructor` in **Solidity**. Unlike other languages like Java where it shares the same name as the class.
- In this example the `()` are left empty. This means it doesn't receieve any **parameters**.
- Think of **parameters** as placeholders for future user inputs.

```solidity
contract Constructor3 {
  string public name;

  constructor(string memory _name) {
    name = _name;
  }
}
```

- The parameter receives an `_` not because it is needed, but rather a way to tell the difference between the two variables.
- Inside the **function expression**, `name` refers to the **state variable**, and that equals `_name`, the `contructors` **parameter**.
- Again, think of the `_name` **parameter** as a placeholder, waiting to receive an end users information they will put in later.
- Otherwise all data would have to be hardcoded in the **constructors expression**.

---

#### Payable Constructors

You can send in cryptocurrency whenever the `smart contract` is deployed.
This is to avoid having to do multiple steps of creating the `smart contract`, then having to send cryptocurrency in a separate transaction.

```solidity
contract Constructors4 {
  string public name;

  constructor() payable {
    name = 'Example 4';
  }
}
```

- This will send `Ether`, the native coin of Ethereum.
- The `Ether` balance will be stored inside the `smart contract` itself.
- Constructors are `public` by default. Do **not** set `visibility modifiers` unto them.

---

#### Inheritance
