In Solidity, the `fallback` and `receive` functions are special functions that enable a contract to handle Ether transfers and interact with messages that do not match any other function signature in the contract. They play a crucial role in how contracts behave when they receive Ether or when they are called without data.

### `fallback` Function
The `fallback` function is a special function in Solidity that is executed when:
- A contract is called with a function signature that does not match any existing function in the contract.
- Ether is sent to the contract, but the `receive` function is not present, or the `receive` function is not `payable`.

**Key Characteristics of the `fallback` Function:**
- It does not have a name.
- It does not take any arguments and does not return anything.
- It is either external or public.
- It can be marked as `payable` to accept Ether; otherwise, the contract cannot receive Ether through this function.
- It is usually limited to 2300 gas when called due to `transfer` or `send` methods, making it suitable only for simple operations.

**Syntax:**
```solidity
fallback() external payable {
    // custom logic
}
```

### `receive` Function
The `receive` function is another special function introduced in Solidity 0.6.0, which is specifically designed to handle plain Ether transfers. The `receive` function is called when:
- The contract receives Ether without any data (i.e., no function call or data is provided in the transaction).
- The contract has a `receive` function defined and it is marked as `payable`.

**Key Characteristics of the `receive` Function:**
- It does not have a name.
- It does not take any arguments and does not return anything.
- It must be external and `payable`.
- It is used exclusively to receive Ether when no data is sent.

**Syntax:**
```solidity
receive() external payable {
    // custom logic for receiving Ether
}
```

### How `fallback` and `receive` Work Together
- If a contract has a `receive` function defined, it will be called whenever Ether is sent to the contract without any data.
- If there is no `receive` function, or if Ether is sent with data that does not match any function signature, the `fallback` function will be triggered.

### Examples

#### Example 1: Basic `fallback` and `receive` Functions
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract EtherReceiver {
    // Event to log received Ether
    event Received(address sender, uint amount);

    // `receive` function to handle plain Ether transfers
    receive() external payable {
        emit Received(msg.sender, msg.value);
    }

    // `fallback` function to handle calls with non-matching function signatures
    fallback() external payable {
        emit Received(msg.sender, msg.value);
    }

    // Function to check the balance of the contract
    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```
- In this contract:
  - The `receive` function is called when Ether is sent to the contract without any data.
  - The `fallback` function is called when Ether is sent with data that does not match any existing function signature.
  - Both functions are `payable`, meaning the contract can accept Ether in either case.

#### Example 2: Handling Calls Without Ether
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract FallbackExample {
    event FallbackCalled(address sender, uint value, bytes data);

    // `fallback` function handles all non-matching function calls
    fallback() external payable {
        emit FallbackCalled(msg.sender, msg.value, msg.data);
    }

    // Normal function to show regular calls
    function normalFunction() public pure returns (string memory) {
        return "Normal function called";
    }
}
```
- In this example:
  - The `fallback` function is used to handle calls that do not match any other function signatures in the contract.
  - It logs the sender, the amount of Ether sent, and any data that was passed with the call.

#### Example 3: `fallback` Function Without `payable`
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract NonPayableFallback {
    event FallbackCalled(address sender, uint value, bytes data);

    // `fallback` function without `payable` modifier
    fallback() external {
        emit FallbackCalled(msg.sender, 0, msg.data);
    }

    // Function to check the contract's balance
    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```
- In this contract:
  - The `fallback` function is not `payable`, meaning it cannot accept Ether.
  - If someone tries to send Ether to this contract, the transaction will fail.

### Summary
- The `receive` function is a simple way to handle Ether transfers without data. It's specifically for receiving Ether.
- The `fallback` function is a more general-purpose function that handles non-matching calls and can optionally receive Ether if marked `payable`.
- Both functions are essential for robust contract design, allowing your contract to handle unexpected interactions and plain Ether transfers gracefully.