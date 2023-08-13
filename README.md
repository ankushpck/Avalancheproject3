# Avalanche Project 3
# Custom Token Smart Contract Deployment Guide

This  will walk through the process of creating a smart contract to deploy your own token using either HardHat or Remix. The contract will have the following functionality:

1. **Only contract owner can mint tokens**
2. **Any user can transfer tokens**
3. **Any user can burn tokens**

## Prerequisites

- Node.js and npm installed (for HardHat)
- Basic understanding of Ethereum and Solidity

## Steps

### 1. Set Up our Environment

#### Using Remix

1. Open Remix in your web browser: https://remix.ethereum.org/

2. Create a new Solidity file for your token contract.

### 2. Write the Smart Contract

Create a new Solidity file (e.g., `CustomToken.sol`) and implement the custom token smart contract. we can use the provided code as a starting point. 

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract CustomToken is ERC20, Ownable {
    constructor(string memory name, string memory symbol) ERC20(name, symbol) {}

    // Function to mint tokens (only owner)
    function mint(address to, uint256 amount) external onlyOwner {
        _mint(to, amount);
    }

    // Function to transfer tokens (any user)
    function transfer(address to, uint256 amount) public override returns (bool) {
        require(to != address(0), "Transfer to the zero address");
        _transfer(_msgSender(), to, amount);
        return true;
    }
 
    // Function to burn tokens (any user)
    function burn(uint256 amount) external {
        _burn(msg.sender, amount);
    }
}
The above code is true to my knowledge and will run smoothly
