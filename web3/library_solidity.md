### Solidity Libraries: Concepts and Types

**Libraries in Solidity** are special types of smart contracts that contain reusable code. They are typically used for functions that are common across multiple contracts, allowing you to avoid code duplication. Libraries have several unique properties and use cases.

### Key Features of Libraries:
1. **Stateless:** Libraries cannot hold state, meaning they cannot store data in a way that persists across transactions. All functions within a library are `pure` or `view`, indicating that they do not modify or store any state.

2. **No Ether Handling:** Libraries cannot receive or store Ether.

3. **Cannot be Destroyed:** Libraries cannot be self-destructed (`selfdestruct` is not allowed).

4. **Inheritance:** Libraries cannot inherit from other contracts or libraries, nor can they be inherited.

### Types of Libraries in Solidity:
Solidity libraries can be classified into two types based on how they are deployed and used in contracts:

1. **Internal Libraries:**
   - **Deployment:** Internal libraries are embedded directly into the contract that uses them. When you deploy a contract that uses an internal library, the code of the library is copied into the contract, meaning the library does not need to be deployed separately.
   - **Function Calls:** Functions of internal libraries are called directly as if they were part of the contract.
   - **Gas Efficiency:** This method is more gas-efficient for small libraries since there’s no need for a delegate call.
   - **Example:**

     ```solidity
     pragma solidity ^0.8.0;

     library Math {
         function add(uint a, uint b) internal pure returns (uint) {
             return a + b;
         }
     }

     contract MyContract {
         using Math for uint;

         function example() public pure returns (uint) {
             return 5.add(10); // Calls Math.add(5, 10)
         }
     }
     ```

2. **External Libraries:**
   - **Deployment:** External libraries are deployed separately from the contracts that use them. The contract uses a `delegatecall` to invoke functions from the library.
   - **Function Calls:** Functions are called using a fully qualified name, and a `delegatecall` is used to execute them in the context of the calling contract.
   - **Gas Efficiency:** External libraries can be more gas-efficient for larger libraries because the code isn’t copied into each contract that uses it.
   - **Example:**

     ```solidity
     pragma solidity ^0.8.0;

     library MathLib {
         function multiply(uint a, uint b) external pure returns (uint) {
             return a * b;
         }
     }

     contract MyContract {
         function multiply(uint a, uint b) public pure returns (uint) {
             return MathLib.multiply(a, b);
         }
     }
     ```

### Using Libraries with `using for`:

Solidity provides a convenient way to attach library functions to a type using the `using for` directive.

**Example:**

```solidity
pragma solidity ^0.8.0;

library ArrayLib {
    function find(uint[] storage arr, uint x) internal view returns (uint) {
        for (uint i = 0; i < arr.length; i++) {
            if (arr[i] == x) {
                return i;
            }
        }
        revert("Not Found");
    }
}

contract Test {
    using ArrayLib for uint[];

    uint[] data;

    function append(uint x) public {
        data.push(x);
    }

    function find(uint x) public view returns (uint) {
        return data.find(x); // Library function find is used
    }
}
```

### Summary:

- **Internal Libraries:** Integrated into the contract that uses them, offering gas efficiency for small libraries.
- **External Libraries:** Deployed separately and called via `delegatecall`, providing benefits for large libraries where code reuse across contracts is needed.
- **Libraries cannot hold state or Ether and cannot be self-destructed.**

This approach to using libraries in Solidity helps in modularizing code and promoting reuse while maintaining a high level of security and efficiency.