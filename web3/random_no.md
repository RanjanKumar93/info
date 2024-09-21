Generating truly random numbers in Solidity is a challenge because blockchains are deterministic systems, making it difficult to ensure randomness without external sources. Here's a safer approach to generating randomness in Solidity:

### 1. **Chainlink VRF (Verifiable Random Function):**
   Chainlink's VRF is the industry standard for generating random numbers on-chain. It provides a provably fair and tamper-proof source of randomness.

   - **Pros:** Secure, tamper-proof, decentralized.
   - **Cons:** Requires Chainlink integration and incurs a fee in LINK tokens.

   **Implementation:**

   ```solidity
   // SPDX-License-Identifier: MIT
   pragma solidity ^0.8.0;

   import "@chainlink/contracts/src/v0.8/VRFConsumerBase.sol";

   contract RandomNumberConsumer is VRFConsumerBase {
       bytes32 internal keyHash;
       uint256 internal fee;
       uint256 public randomResult;

       constructor()
           VRFConsumerBase(
               0x514910771AF9Ca656af840dff83E8264EcF986CA, // VRF Coordinator
               0x514910771AF9Ca656af840dff83E8264EcF986CA  // LINK Token
           )
       {
           keyHash = 0x6c3699283bda56ad74f6b855546325b68d482e983852a035b7d9c9b35f4fd7d8;
           fee = 0.1 * 10 ** 18; // 0.1 LINK
       }

       function getRandomNumber() public returns (bytes32 requestId) {
           require(LINK.balanceOf(address(this)) >= fee, "Not enough LINK");
           return requestRandomness(keyHash, fee);
       }

       function fulfillRandomness(bytes32 requestId, uint256 randomness) internal override {
           randomResult = randomness;
       }
   }
   ```

   **Explanation:**
   - You request randomness from Chainlink by calling `getRandomNumber`.
   - The result is provided in `fulfillRandomness`, and you can use the `randomResult` in your contract.

### 2. **Oraclize (Provable):**
   Another solution is using the Oraclize service, which provides off-chain randomness. Like Chainlink, this is an external service and requires fees.

   - **Pros:** Fair and reliable randomness.
   - **Cons:** Fees and reliance on an external service.

   **Example:**
   ```solidity
   // SPDX-License-Identifier: MIT
   pragma solidity ^0.8.0;

   import "github.com/provable-things/ethereum-api/provableAPI.sol";

   contract RandomNumber is usingProvable {
       uint256 public randomNumber;

       function __callback(bytes32 _queryId, string memory _result) public override {
           require(msg.sender == provable_cbAddress());
           randomNumber = uint256(keccak256(abi.encodePacked(_result)));
       }

       function getRandomNumber() public payable {
           provable_query("WolframAlpha", "random number between 1 and 100");
       }
   }
   ```

### 3. **Commit-Reveal Schemes:**
   A more decentralized way of generating random numbers is to use a commit-reveal scheme. Participants submit commitments and then reveal them, with the final number being generated based on the revealed values. This is more complex to implement but can work in certain use cases.

   - **Pros:** Trustless and decentralized.
   - **Cons:** Susceptible to manipulation if not properly implemented, and it requires participation from multiple parties.

### 4. **Block Hash Manipulation (Unsafe):**
   A naive approach is using block hashes, timestamps, or other block parameters, but these can be manipulated by miners.

   ```solidity
   function getRandomNumber() public view returns (uint256) {
       return uint256(keccak256(abi.encodePacked(block.difficulty, block.timestamp, block.number)));
   }
   ```

   **Caution:** Avoid this method for any serious use cases as it is insecure.

### **Conclusion:**
The safest and most reliable way to generate random numbers in Solidity is using Chainlink VRF. It ensures that your randomness is tamper-proof and verifiable, which is crucial for use cases like lotteries, gaming, or any application where fair random generation is critical.