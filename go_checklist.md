# 1. Don't calculate constants
```solidity
uint256 constant INT_MAX = uint256(type(int256).max);
int256 constant MIN_BALANCE = 10**12;
int256 constant MULTIPLIER = 1e18;
```

# 2. Do not initialize variables with default values
```solidity
bool constant FEE_DOWN = false;
Address SampleAddress = 0;
```

# 3. OR in `if-`condition can be rewritten to two single if conditions
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