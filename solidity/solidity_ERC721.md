### ERC721 Tokens: A Comprehensive Guide

**ERC721** is a standard for non-fungible tokens (NFTs) on the Ethereum blockchain. Unlike ERC20 tokens, which are fungible and interchangeable, ERC721 tokens are unique, making them ideal for applications such as digital art, collectibles, and gaming assets.

### Key Concepts

1. **Non-Fungibility**: Each ERC721 token is unique. Two tokens are not interchangeable, even if they have the same metadata or attributes. Each token has a unique `tokenId`.

2. **Ownership**: ERC721 tokens are owned by Ethereum addresses. The ownership of a token is tracked on-chain, allowing the owner to transfer, sell, or use the token in various applications.

3. **Metadata**: ERC721 tokens can have associated metadata, typically a URI pointing to a JSON file. This file contains information about the token, such as a description, image, and attributes. This metadata is crucial for use cases like digital art.

4. **Transfer**: ERC721 tokens can be transferred from one owner to another using the `transferFrom` and `safeTransferFrom` functions. These functions ensure that the recipient is capable of receiving ERC721 tokens.

5. **Minting & Burning**: New tokens can be created (minted) and destroyed (burned). Minting typically involves assigning a new `tokenId` to an address, while burning removes the token from circulation.

6. **Approval & Allowances**: Similar to ERC20, ERC721 supports approval mechanisms. An owner can approve another address to manage their token via the `approve` function. The `setApprovalForAll` function allows a user to approve or revoke approval for all tokens owned by them.

### ERC721 Interface

The ERC721 standard consists of several functions and events. Here is the basic interface:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface IERC721 {
    event Transfer(address indexed from, address indexed to, uint256 indexed tokenId);
    event Approval(address indexed owner, address indexed approved, uint256 indexed tokenId);
    event ApprovalForAll(address indexed owner, address indexed operator, bool approved);

    function balanceOf(address owner) external view returns (uint256 balance);
    function ownerOf(uint256 tokenId) external view returns (address owner);
    function safeTransferFrom(address from, address to, uint256 tokenId) external;
    function transferFrom(address from, address to, uint256 tokenId) external;
    function approve(address to, uint256 tokenId) external;
    function getApproved(uint256 tokenId) external view returns (address operator);
    function setApprovalForAll(address operator, bool _approved) external;
    function isApprovedForAll(address owner, address operator) external view returns (bool);
    function safeTransferFrom(address from, address to, uint256 tokenId, bytes calldata data) external;
}
```

This interface defines the core ERC721 functionality.

### ERC721 Full Implementation Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyNFT is ERC721, Ownable {
    uint256 private _tokenIdCounter;

    constructor() ERC721("MyNFT", "MNFT") {}

    function mintNFT(address to) public onlyOwner {
        _safeMint(to, _tokenIdCounter);
        _tokenIdCounter++;
    }

    function _baseURI() internal view virtual override returns (string memory) {
        return "https://api.example.com/metadata/";
    }
}
```

**Explanation**:

- **ERC721**: The contract inherits from the OpenZeppelin implementation of ERC721, which handles most of the standard's functionality.
- **Ownable**: The `Ownable` contract restricts certain functions (like minting) to the contract owner.
- **mintNFT**: This function allows the contract owner to mint a new NFT and assigns it a unique `tokenId`.
- **\_baseURI**: This function returns the base URI for token metadata.

### Advanced Features

1. **Enumerable**: The ERC721Enumerable extension allows enumeration of tokens owned by an address, as well as enumeration of all tokens on the contract.

2. **Metadata**: The ERC721Metadata extension adds support for token names, symbols, and URIs for token metadata.

3. **Safe Transfers**: The `safeTransferFrom` function ensures that tokens are transferred only to addresses that can handle ERC721 tokens. This prevents tokens from being sent to contracts that do not implement ERC721 handling.

### Example with Enumerable and Metadata Extensions

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/extensions/ERC721Enumerable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyAdvancedNFT is ERC721Enumerable, Ownable {
    uint256 private _tokenIdCounter;

    constructor() ERC721("MyAdvancedNFT", "MANFT") {}

    function mintNFT(address to) public onlyOwner {
        _safeMint(to, _tokenIdCounter);
        _tokenIdCounter++;
    }

    function _baseURI() internal view virtual override returns (string memory) {
        return "https://api.example.com/metadata/";
    }

    function totalSupply() public view override returns (uint256) {
        return _tokenIdCounter;  // Override totalSupply for simplicity
    }

    function tokensOfOwner(address owner) public view returns (uint256[] memory) {
        uint256 tokenCount = balanceOf(owner);
        uint256[] memory tokens = new uint256[](tokenCount);
        for (uint256 i = 0; i < tokenCount; i++) {
            tokens[i] = tokenOfOwnerByIndex(owner, i);
        }
        return tokens;
    }
}
```

**Explanation**:

- **ERC721Enumerable**: Adds functions to enumerate tokens owned by an address and tokens in the contract.
- **tokensOfOwner**: Returns an array of token IDs owned by a specific address.

### Key Functions

- **balanceOf(address owner)**: Returns the number of tokens owned by `owner`.
- **ownerOf(uint256 tokenId)**: Returns the owner of the `tokenId`.
- **approve(address to, uint256 tokenId)**: Approves `to` to manage `tokenId`.
- **transferFrom(address from, address to, uint256 tokenId)**: Transfers `tokenId` from `from` to `to`.
- **safeTransferFrom(address from, address to, uint256 tokenId)**: Safely transfers `tokenId`.
- **\_safeMint(address to, uint256 tokenId)**: Mints a new token to `to` with `tokenId`.

### Example: Metadata Structure (Off-Chain)

The metadata for an ERC721 token is typically stored off-chain and referenced by a URI. Here's an example of the metadata JSON:

```json
{
  "name": "My NFT",
  "description": "This is my first NFT",
  "image": "https://api.example.com/images/1.png",
  "attributes": [
    {
      "trait_type": "Background",
      "value": "Blue"
    },
    {
      "trait_type": "Eyes",
      "value": "Green"
    }
  ]
}
```

This metadata file would be hosted at the URI returned by `_baseURI` and concatenated with the token ID.

### Use Cases for ERC721

1. **Digital Art**: Artists can create unique digital art pieces as ERC721 tokens, which can be bought, sold, and traded.
2. **Collectibles**: Companies can issue collectible items, such as trading cards or in-game assets, as ERC721 tokens.
3. **Real Estate**: Property ownership can be tokenized, where each ERC721 token represents a unique piece of real estate.

### Conclusion

ERC721 is the go-to standard for creating non-fungible tokens on Ethereum. It allows developers to create unique assets that can be owned, transferred, and integrated into decentralized applications. The OpenZeppelin library provides a robust and secure implementation of ERC721, enabling developers to focus on building their application logic.
