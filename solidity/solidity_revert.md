In Solidity, `revert` is used to stop the execution of a function, undo all state changes, and optionally provide an error message. It’s typically used in situations where an operation cannot be completed due to invalid input, unmet conditions, or any other issue.

When `revert` is called, it:

1. Halts the function’s execution.
2. Reverts all changes made to the blockchain during the transaction.
3. Optionally returns a custom error message to the caller.

### Basic Usage of `revert`

The simplest way to use `revert` is to call it when a condition fails.

#### Example:

```solidity
pragma solidity ^0.8.0;

contract RevertExample {
    function checkEven(uint _num) public pure returns (string memory) {
        if (_num % 2 != 0) {
            revert("Number is not even.");
        }
        return "Number is even.";
    }
}
```

**Explanation:**

- The `checkEven` function checks if a number is even. If it’s not, the `revert` statement is executed with the error message `"Number is not even."`
- When `revert` is triggered, any gas left is refunded to the caller, and the state reverts to what it was before the transaction.

### `revert` with Custom Error Messages

Solidity allows you to include custom error messages in `revert` calls. These error messages are returned to the caller and help with debugging by providing information on why the transaction failed.

#### Example:

```solidity
pragma solidity ^0.8.0;

contract Auction {
    address public highestBidder;
    uint public highestBid;

    function bid(uint amount) public {
        if (amount <= highestBid) {
            revert("Bid is too low.");
        }

        highestBid = amount;
        highestBidder = msg.sender;
    }
}
```

**Explanation:**

- If a user submits a bid that is lower than or equal to the current highest bid, the transaction is reverted with the message `"Bid is too low."`
- No changes to `highestBid` or `highestBidder` are made if the condition fails.

### `require` vs. `revert`

Both `require` and `revert` can be used to trigger errors in Solidity. However, `require` is typically used when checking preconditions (before executing the function logic), while `revert` is used when conditions deeper inside the function logic fail.

#### Example using `require`:

```solidity
pragma solidity ^0.8.0;

contract RequireVsRevert {
    function checkPositive(int _num) public pure {
        require(_num > 0, "Number must be positive.");
    }
}
```

**Key Differences:**

- `require` is more commonly used for input validation.
- `revert` is used when handling more complex conditional logic deeper in the code.

### Gas Refund

When a transaction is reverted, the remaining gas is refunded to the caller. However, any gas already used for computations before the `revert` call is consumed. This is why Solidity developers aim to trigger `revert` as early as possible to minimize wasted gas.

#### Example:

```solidity
pragma solidity ^0.8.0;

contract GasRefundExample {
    uint public counter;

    function increment(uint _num) public {
        // Check condition early to avoid unnecessary computation
        if (_num == 0) {
            revert("Number cannot be zero.");
        }

        // Complex computations
        for (uint i = 0; i < _num; i++) {
            counter++;
        }
    }
}
```

**Explanation:**

- The `revert` is triggered early if `_num` is zero, preventing unnecessary computation and saving gas.

### `revert` with Custom Errors (Solidity 0.8+)

Starting from Solidity 0.8, you can define custom errors. Custom errors are more efficient than using strings in `revert` because they consume less gas and can carry more structured information.

#### Example of Custom Errors:

```solidity
pragma solidity ^0.8.0;

contract CustomErrorExample {
    error InvalidBid(uint currentBid, uint newBid);

    uint public highestBid;

    function bid(uint amount) public {
        if (amount <= highestBid) {
            revert InvalidBid(highestBid, amount); // Custom error
        }

        highestBid = amount;
    }
}
```

**Explanation:**

- `InvalidBid` is a custom error that contains two parameters: the current highest bid and the new bid.
- When `revert` is called with a custom error, it passes structured data instead of a string message, making it more gas-efficient.

### `revert` in Try-Catch

Solidity supports error handling using `try-catch` blocks. This is particularly useful when interacting with external contracts, allowing you to catch and handle failures.

#### Example:

```solidity
pragma solidity ^0.8.0;

contract Caller {
    function callAnotherContract(address _contract) public {
        try SomeContract(_contract).someFunction() {
            // Success logic
        } catch {
            revert("Call to external contract failed.");
        }
    }
}

contract SomeContract {
    function someFunction() public pure returns (string memory) {
        return "Hello from SomeContract!";
    }
}
```

**Explanation:**

- The `Caller` contract tries to call the `someFunction` of another contract (`SomeContract`).
- If the call fails, the `catch` block is executed, and `revert` is called with the error message `"Call to external contract failed."`

### `assert` vs. `revert`

- `assert`: Used for internal errors or to check for conditions that should never fail (invariant checks). If an `assert` statement fails, it causes a **panic** (and consumes all gas).
- `revert`: Used to handle failures in business logic or external interactions, refunding remaining gas.

#### Example:

```solidity
pragma solidity ^0.8.0;

contract AssertExample {
    uint public total;

    function add(uint _value) public {
        total += _value;
        // Check an invariant with assert
        assert(total >= _value); // This should never fail
    }
}
```

**Explanation:**

- `assert` is used to check conditions that should never occur under normal circumstances. If an `assert` statement fails, it indicates a serious bug or issue in the contract logic.

### Summary of `revert`:

- **`revert`** stops execution, reverts all state changes, and can return an optional error message.
- **Custom Errors**: Custom errors (introduced in Solidity 0.8) are a more gas-efficient way of using `revert` with error messages.
- **`revert` vs `require`**: Use `require` for input validation and `revert` for more complex failure logic.
- **Gas Refund**: Remaining gas is refunded, but already used gas is consumed.

These are the essential details about `revert` in Solidity.
