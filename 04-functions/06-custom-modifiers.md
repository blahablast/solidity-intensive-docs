## Custom Modifiers

---

A common use for `custom` is when you see an `ownable` pattern.
It's called `access control`. This is where you can **restrict** who can call a certain function.

---

```solidity
contract Functions6 {
  address private owner;

  constructor() {
    owner = msg.sender;
  }

  function setName1(string memory _name) public {
    require(msg.sender == owner, 'caller must be owner');
    name = _name;
  }
}
```

- `msg.sender` is the person **deploying** the contract to the Blockchain.
- This is getting saved to the `private` `state variable` `owner`.
- `setName1` is attempting to set a variable called `name` to the `parameter` `_name`.
- Before this happens though, we are calling `require`.
- `require` takes in two arguments.
- First is `msg.sender` must `==` the `state variable` `owner`.
- Second is just a message if it **doesn't** equal owner and evaluates to `false`.
- This is basically **authentication** at the `contract` level.

---

#### The Custom Way

The above example is fine for a single function, but isn't efficient for multiple functions.
So what we can do is create our own `modifier` function.

```solidity
contract Functions6 {
  address private owner;
  string public name = '';

  constructor() {
    owner = msg.sender;
  }

  modifier onlyOwner {
    require(msg.sender == owner, 'caller must be owner');
    _;
  }

  function setName1(string memory _name) onlyOwner public {
    name = _name;
  }
}
```

- All we did here was remove the `require` from the `setName1` function and created a `modifier` function.
- Now it can be used for any other function that needs it in our `contract`.
- `onlyOwner` must be called in the `setName1` **function signature**.
- The `_;` comes after the `require` to represent the rest of the code that will be called on a function that has `onlyOwner` in the **function signature**.
- You always want to call the `require` first, for proper **authentication** purposes.
- You can also call multiple `modifiers` on a **function signature**.
  **quick aside** - you will notice a `custom modifier` will be a different color than a `built in modifier` from **Solidity**.
