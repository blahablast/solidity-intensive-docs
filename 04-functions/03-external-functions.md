## Working with External functions

---

Not much of a difference here, but very important to understand.

```solidity
contract Functions3 {
  uint public count;

  function increment() public {
    count = addNumbers(count, 1);
  }
}

function addNumbers(uint a, uint b) pure returns(uint) {
  return a + b;
}
```

You will notice that `addNumbers` exists outside of the `contract` `Functions3`.
But it is being called within the function `addNumbers` which **is** inside the `contract`.

---

#### Why this is possible?

This is possible because `addNumbers` **doesn't** have `internal` within the `function signature`.
