## Functions

---

```solidity
string name = 'Example 1';

function setName(string memory _name) public {
  name = _name;
}

function getName() public view returns(string memory) {
  return name;
}

function resetName() public {
  name = 'Example 1';
}
```

We have a `state variable` called name.
This means it is written and stored to the blockchain.

---

#### Gas

All `gas` on Ethereum is paid in `Ether`. The native coin.
`Gas` exists to prevent spam on the network.

---

#### setName

`setName` function sets the name on the blockchain.
So this means it is writing to the blockchain, updating its state. This requires `gas`.

---

#### getName

`getName` is a _read only_ function.
This doesn't require any `gas`. It is free.

---

#### Test to prove it works

```javascript
it('demonstrates read functions are free', async () => {
  let balanceBefore = await ethers.provider.getBalance(deployer.address)
  await contract.getName()
  let balanceAfter = await ethers.provider.getBalance(deployer.address)
  expect(balanceBefore).to.equal(balanceAfter)
})
```
