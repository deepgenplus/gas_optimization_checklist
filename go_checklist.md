### 1. Don't calculate constants
```solidity
uint256 constant INT_MAX = uint256(type(int256).max);
int256 constant MIN_BALANCE = 10**12;
int256 constant MULTIPLIER = 1e18;
```

### 2. Do not initialize variables with default values
```solidity
bool constant FEE_DOWN = false;
Address SampleAddress = 0;
```

### 3. OR in `if-`condition can be rewritten to two single if conditions
```solidity
if (py_init >= MAX_PRICE_VALUE || py_final >= MAX_PRICE_VALUE) return 1;
if (px_init <= MIN_PRICE_VALUE || px_final <= MIN_PRICE_VALUE) return 1;
```
This suggests, that conditions should be rewritten to:
```solidity
if (py_init >= MAX_PRICE_VALUE) return 1;
if (py_final >= MAX_PRICE_VALUE) return 1;
if (px_init <= MIN_PRICE_VALUE) return 1;
if (px_final <= MIN_PRICE_VALUE) return 1;
```

### 4. Use `!= 0` instead of `> 0` for unsigned integer comparison
When dealing with unsigned integer types, comparisons with `!= 0` are cheaper then with `> 0`.

![](https://global.discourse-cdn.com/business6/uploads/zeppelin/original/2X/3/363a367d6d68851f27d2679d10706cd16d788b96.png)

> [!IMPORTANT]
> To update this with using at least 0.8.6 there is no difference in gas usage with `!= 0` or `> 0`

### 5. Use shift right/left instead of division/multiplication if possible
While the `DIV` / `MUL` opcode uses 5 gas, the `SHR` / `SHL` opcode only uses 3 gas. Furthermore, beware that Solidity's division operation also includes a division-by-0 prevention which is bypassed using shifting. Eventually, overflow checks are never performed for shift operations as they are done for arithmetic operations. Instead, the result is always truncated.
![](https://global.discourse-cdn.com/business6/uploads/zeppelin/original/2X/c/c427c82eac6126e75c9f4092a0354b0fa56840a2.jpeg)


