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

`Constructors` can `inherit` from base contracts.

```solidity
contract Parent1 {
  string public name;

  constructor() {
    name = 'Example 5';
  }
}

contract Constructors5 is Parent1 {
  string public description = 'This contract inherits from Parent 1';
  // Do not declare a constructor here
}
```

- Saying `is` `Parent1` signifies you are inheriting from another `contract`.
- No need to add a `constructor` to the `child` contract. We get to use the `parent` `constructor`.

`Constructors` can also extend behavior from `parent` `constructors`.

```solidity
contract Parent2 {
  string public name;

  constructor(string memory _name) {
    name = _name;
  }
}

contract Constructors6 is Parent2 {
  string public description;

  constructor(string memory _name, string memory _description) Parent2(_name) {
    description = _description;
  }
}
```

1. Inheriting Parent Constructor Behavior:

- When we want the `parent constructor` behavior, we explicitly call it in the `child constructor`.
- This is done by using the `parent` name and passing the required **parameters**: `Parent2(_name)`.

2. Extending Behavior:

- In the `child constructor`, we add additional **parameters** and logic to extend the `parent` behavior.
- For example, the description **parameter** is specific to `Constructors6` and is `initialized` in its `constructor`.

3. Parameter Passing:

- `Parent2(_name)` refers to the `parent constructor` and passes the `_name` **parameter** from the `child constructor` to it.
- This ensures the name **state variable** in `Parent2` is properly `initialized` when deploying `Constructors6`.
