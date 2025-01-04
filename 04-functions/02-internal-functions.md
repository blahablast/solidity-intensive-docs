## Working with Internal functions

---

```solidity
contract Functions2 {
  uint public count;

  function add(uint a, uint b) internal pure returns(uint) {
    return a + b;
  }
}
```

This function is `internal`, which means it can **only** be used within the smart contract `Functions2`.
It can be used within another `function` inside this `Functions2`**smart contract** like this:
`pure`, which you see in the `function signature`, disallows **modification** or **access** of state.
`view`, not in this example, is similar to `pure`, but **only** disallows **modification** of state.

```solidity
function increment() public {
  count = add(count, 1);
}
```

As you can see here, `add` is being called inside a new function called `increment`.
It must exist inside the same **smart contract** of `Functions2` because we made it `internal`.
A `contract` is very similar to a **class** in Java.

---

#### Test to prove it works

```javascript
describe('Example 2', () => {
  let contract

  beforeEach(async () => {
    const Contract = await ethers.getContractFactory('Functions2')
    contract = await Contract.deploy()
  })

  it('calls a function inside another function', async () => {
    await contract.increment()
    expect(await contract.count()).to.equal(1)
  })
})
```

In this test, inside our `beforeEach` you must first grab the contract with `getContractFactory`.
Storing that into a variable called `Contract` to be used on the next line...
Then we `deploy` that `Contract`, which gets stored into it's own variable called `contract`.
Don't get confused by the Upper & Lower casings. They exist like that for a reason.
Simply so they are not exactly the same and overwriting one another.
