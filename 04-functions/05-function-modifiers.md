## Function Modifiers

---

You can read about there [here](https://docs.soliditylang.org/en/latest/contracts.html) on the official site.

In simple terms, **modifiers** change behavior of functions.

We will only go over the common ones because too much info isn't necessary.

- `pure`: Disallows modification or access of state.
- `view`: Disallows modification of state.
- `payable`: Allows them to receive `Ether` together with a call.

---

#### view

```solidity
contract Functions5 {
  string public name = 'Example 5';
  uint public balance;

  function getName() public view returns(string memory) {
    return name;
  }
}
```

This is a **read only** function.
You will not pay any `gas`. You are **not** writing to the Blockchain.
If you try to **modify** the **state** in a `view` function, it **won't** work.
You **can** access the **state**.

---

#### pure

```solidity
contract Functions5 {
  string public name = 'Example 5';
  uint public balance;

  function add(uint a, uint b) public pure returns(uint) {
    return a + b;
  }
}
```

Similar to `view` is `pure`.
Just like `view`, it **cannot** **modify** the **state**.
Difference is `pure` **cannot** access the **state**.
We are **not** affecting the `state variables` in any way with the `add` function because of the `pure` `modifier`.
You **cannot** even read the `state variables`. It is very strict!

---

#### payable

```solidity
contract Functions5 {
  string public name = 'Example 5';
  uint public balance;

  function pay() public payable {
    balance = msg.value;
  }
}
```

`payable` means the function can **accept** cryptocurrency whenever we create the transaction.
`payable` is what **allows** you to even use `msg.value` inside this function.

---

`msg.value` is a property of the `msg` global object.</summary>

- It is a **type** of `uint256`.
- The value in denominated in `wei`, the smallest unit of `Ether`. (1 `Ether` = 10^18 `wei`)
- It is used to check how much `Ether` was **sent** with the transaction.
- **only** works for functions that are `payable`.
