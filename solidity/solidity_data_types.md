In Solidity, data types define how information is stored and manipulated within smart contracts. Solidity supports various types of data, including value types, reference types, and complex types.

### 1. **Value Types**

Value types are stored directly in the memory or storage. They are copied by value, which means when you assign them to another variable, the entire value is copied.

#### 1.1 **Booleans**

Booleans are used to represent logical true or false values.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract BooleanExample {
    bool public isActive = true;

    function deactivate() public {
        isActive = false;
    }
}
```

#### 1.2 **Integers**

Solidity supports both signed (`int`) and unsigned (`uint`) integers.

- **`uint`**: An unsigned integer (only positive) that can be of different sizes (`uint8`, `uint16`, ..., `uint256`).
- **`int`**: A signed integer (positive and negative) that can also have various sizes (`int8`, `int16`, ..., `int256`).

```solidity
// Unsigned integer
uint256 public positiveNumber = 100;  // Ranges from 0 to 2^256 - 1

// Signed integer
int256 public negativeNumber = -100;  // Ranges from -2^255 to 2^255 - 1
```

#### 1.3 **Address**

An `address` type is used to store Ethereum addresses. Solidity also introduced `address payable`, which allows addresses to send Ether.

```solidity
address public owner = msg.sender;  // Stores the address of the contract deployer

function sendEther(address payable _to) public payable {
    _to.transfer(msg.value);  // Sends Ether to the specified address
}
```

#### 1.4 **Enums**

Enums are user-defined types that represent a set of predefined constants.

```solidity
contract EnumExample {
    enum Status { Pending, Shipped, Delivered }

    Status public currentStatus = Status.Pending;

    function ship() public {
        currentStatus = Status.Shipped;
    }

    function getStatus() public view returns (Status) {
        return currentStatus;
    }
}
```

### 2. **Reference Types**

Reference types do not store the actual value but reference the data stored elsewhere. These types include arrays, mappings, and structs.

#### 2.1 **Arrays**

Arrays can be dynamic or fixed in size, and they can hold elements of any type.

- **Fixed-size array**:

```solidity
uint[3] public fixedArray = [1, 2, 3];
```

- **Dynamic array**:

```solidity
uint[] public dynamicArray;

function addElement(uint _element) public {
    dynamicArray.push(_element);
}
```

#### 2.2 **Structs**

Structs allow you to group different variables under a single type. This is useful for creating complex data types.

```solidity
struct Person {
    string name;
    uint age;
}

Person public person;

function createPerson(string memory _name, uint _age) public {
    person = Person(_name, _age);
}
```

#### 2.3 **Mappings**

Mappings are like hash tables in other languages and allow for key-value pair associations. They are typically used for storing balances or user data.

```solidity
mapping(address => uint) public balances;

function setBalance(address _addr, uint _balance) public {
    balances[_addr] = _balance;
}

function getBalance(address _addr) public view returns (uint) {
    return balances[_addr];
}
```

### 3. **Special Types**

There are some special types in Solidity, like functions, literals, and more.

#### 3.1 **Functions**

Solidity allows functions to be treated as types, meaning you can pass them around like variables.

```solidity
function add(uint _a, uint _b) public pure returns (uint) {
    return _a + _b;
}

function example() public view {
    function (uint, uint) pure returns (uint) myFunction = add;
    uint result = myFunction(1, 2);  // result = 3
}
```

#### 3.2 **Bytes**

Solidity provides two types of byte arrays: `bytes` (dynamic) and `bytes1` to `bytes32` (fixed-size).

```solidity
bytes public dynamicBytes; // Dynamic byte array

function setBytes(bytes memory _data) public {
    dynamicBytes = _data;
}

bytes32 public fixedBytes; // Fixed-size byte array (32 bytes)
```

#### 3.3 **Strings**

Strings in Solidity are arrays of bytes, but they do not have many features like string manipulation.

```solidity
string public name = "Solidity";
```

### 4. **Storage and Memory Keywords**

In Solidity, reference types like arrays and structs can exist in storage or memory. Storage is used for persistent data on the blockchain, while memory is used for temporary variables.

- **Memory**: Variables stored in memory are temporary and erased between external function calls.
- **Storage**: Variables stored in storage are persistent and stored on the blockchain.

```solidity
struct Data {
    uint x;
    uint y;
}

Data public storedData;

function changeData(uint _x, uint _y) public {
    Data memory tempData = Data(_x, _y);  // Stored in memory, not persisted
    storedData = tempData;  // Now persists in storage
}
```

### 5. **Literal Types**

Solidity supports literal types like integers, strings, and booleans that are used directly.

```solidity
uint public literalValue = 10;  // Integer literal
```

### Summary

- **Value Types**: Stored directly in memory (e.g., `bool`, `uint`, `int`, `address`).
- **Reference Types**: Stored by reference (e.g., arrays, mappings, structs).
- **Special Types**: Include functions, `bytes`, `string`, and literals.
- **Memory vs Storage**: Important when dealing with reference types, as `memory` is temporary and `storage` is permanent.

This covers all basic data types in Solidity, how they are used, and key distinctions between memory and storage!
