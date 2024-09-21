Proxy implementation using Hardhat, OpenZeppelin, and Etherscan for verification.

### **Project Overview**

We will build an upgradeable decentralized voting system that allows proposals, voting, and delegate voting. The key aspect will be using a proxy contract to enable upgrades without disrupting the contract's state and address.

### **Steps and Key Concepts**

#### **1. Introduction to Proxy Contracts**

- **Why Proxy Contracts?**
  - Upgradeability: Allows changing the logic of the contract without altering the contract's address or losing data.
  - Proxies separate the storage and logic layers of smart contracts.
- **Types of Proxy Patterns:**
  - **Transparent Proxy:** Most common; admins can upgrade, but they can't interact with the contract logic.
  - **UUPS Proxy:** More gas efficient; the contract itself contains the upgrade logic.
  - **Beacon Proxy:** Allows multiple proxy instances to share the same upgrade logic via a beacon contract.

#### **2. Setting Up the Project**

- **Tools and Dependencies:**
  - Hardhat (for development and deployment)
  - OpenZeppelin (for security and proxy contracts)
  - Etherscan (for verification)
  - VScode (for writing the code)

**Project Initialization:**

```bash
npx hardhat init
npm install @openzeppelin/contracts @openzeppelin/hardhat-upgrades
```

#### **3. Writing the Base Logic Contract**

- Start by creating a basic voting contract that allows users to create proposals and vote.
- Implement the basic logic without proxy, to begin with, so you understand the initial non-upgradable structure.

**`Voting.sol` (Initial Version)**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Voting {
    struct Proposal {
        string description;
        uint voteCount;
    }

    mapping(uint => Proposal) public proposals;
    uint public proposalCount;

    function createProposal(string memory description) public {
        proposals[proposalCount] = Proposal(description, 0);
        proposalCount++;
    }

    function vote(uint proposalId) public {
        proposals[proposalId].voteCount++;
    }
}
```

#### **4. Integrating Proxy Pattern**

- **Transparent Proxy Pattern:**
  - We will use OpenZeppelin’s `TransparentUpgradeableProxy` to manage the upgradeability of the contract.

**Creating the Proxy-Upgradeable Voting Contract:**

1.  Convert the `Voting` contract to be upgradeable by removing the constructor and using the initializer.
2.  Deploy the proxy with the upgradeable contract logic.

**`VotingUpgradeable.sol`**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";

contract VotingUpgradeable is Initializable {
    struct Proposal {
        string description;
        uint voteCount;
    }

    mapping(uint => Proposal) public proposals;
    uint public proposalCount;

    function initialize() public initializer {
        // Initialization logic if needed
    }

    function createProposal(string memory description) public {
        proposals[proposalCount] = Proposal(description, 0);
        proposalCount++;
    }

    function vote(uint proposalId) public {
        proposals[proposalId].voteCount++;
    }
}
```

#### **5. Writing Upgrade Logic**

- Let's introduce delegate voting as a new feature to demonstrate upgrading the logic.

**`VotingV2Upgradeable.sol`**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "./VotingUpgradeable.sol";

contract VotingV2Upgradeable is VotingUpgradeable {
    mapping(address => address) public delegates;

    function delegateVote(address to) public {
        delegates[msg.sender] = to;
    }

    function vote(uint proposalId) public override {
        address delegate = delegates[msg.sender];
        if (delegate != address(0)) {
            proposals[proposalId].voteCount++;
        } else {
            super.vote(proposalId);
        }
    }
}
```

#### **6. Deploying and Managing Upgrades**

- **Deploying the Initial Proxy Contract:**
  - Use Hardhat and OpenZeppelin upgrades plugin for deployment.

```javascript
const { ethers, upgrades } = require("hardhat");

async function main() {
  const Voting = await ethers.getContractFactory("VotingUpgradeable");
  const voting = await upgrades.deployProxy(Voting, [], {
    initializer: "initialize",
  });
  await voting.deployed();
  console.log("Voting deployed to:", voting.address);
}

main();
```

- **Upgrading the Contract:**
  - Once you’ve deployed the first version, upgrade it to `VotingV2Upgradeable`.

```javascript
async function upgrade() {
  const VotingV2 = await ethers.getContractFactory("VotingV2Upgradeable");
  const upgraded = await upgrades.upgradeProxy(existingProxyAddress, VotingV2);
  console.log("Voting upgraded to V2 at:", upgraded.address);
}

upgrade();
```

#### **7. Verifying Contracts on Etherscan**

- After deployment and upgrades, verify the implementation contracts on Etherscan using the Hardhat Etherscan plugin.

```bash
npx hardhat verify --network sepolia DEPLOYED_PROXY_ADDRESS
```

#### **8. Testing and Deployment**

- Write comprehensive unit tests for both versions of the contract.
- Test the upgrade flow to ensure that no data is lost during upgrades.
- Deploy on a test network like Sepolia and interact with the contract.

#### **9. Best Practices and Security**

- **Storage Layout:** Ensure that storage layout changes are handled carefully during upgrades.
- **Access Control:** Implement access control to ensure that only authorized users can upgrade the contract.
- **Testing:** Test thoroughly using both unit tests and integration tests to simulate the upgrade process.

#### **10. Additional Concepts**

- **UUPS Proxies:** Implement a UUPS proxy for more gas-efficient upgrades.
- **Beacon Proxies:** Scale your project by using Beacon proxies to manage multiple voting instances with shared upgrade logic.
