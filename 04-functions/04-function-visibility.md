## Visibility Specifiers

---

`public`: visible externally and internally (creates a `getter function` for storage/state Variables)
`private`: only visible on the current contract
`external`: only visible externally (only for functions)
`internal`: only visible internally

---

#### Public

```solidity
contract Functions4 {
  uint public count;

  function increment1() public {
    count = count + 1;
  }

  function increment2() public {
    increment();
  }
}
```

The main takeaway here is `increment2` is calling `increment` and it works.
This would workout **outside** the `contract` of `Functions4` as well, because the functions are set to `public`.

---

#### Private

```solidity
contract Functions4 {
  uint public count;

  function increment1() public {
    count = count + 1;
  }

  function increment2() public {
    increment();
  }

  function increment3() private {
    count = count + 1;
  }

  function increment4() public {
    increment3();
  }
}
```

This example **works** even though `increment3` is `private`.
It works because they both exist inside the **same** `contract` of `Functions4`.

---

#### External

```solidity
contract Functions4 {
  uint public count;

  function increment1() public {
    count = count + 1;
  }

  function increment2() public {
    increment();
  }

  function increment3() private {
    count = count + 1;
  }

  function increment4() public {
    increment3();
  }

  function increment5() external {
    count = count + 1;
  }
}
```

You **cannot** call `increment5` inside of another function.
This is due to it being `external`. It will not even **compile**.
If you placed `increment5` **outside** of the `contract` `Functions4`, you **can** call it.

---

#### Internal

```solidity
contract Functions4 {
  uint public count;

  function increment1() public {
    count = count + 1;
  }

  function increment2() public {
    increment();
  }

  function increment3() private {
    count = count + 1;
  }

  function increment4() public {
    increment3();
  }

  function increment5() external {
    count = count + 1;
  }

  function increment6() internal {

  }
}
```

You **cannot** call `increment6` **outside** of the `contract` `Functions4`.
Must be **within** the same `contract` of `Functions4`.
You **can** call `increment6` from another function.
You **can** call this from an `inherited` `contract`.
