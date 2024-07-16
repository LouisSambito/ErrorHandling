
# Error Handling

This Solidity project demonstrates the use of require(), assert(), and revert() statements within a smart contract. It serves as an introduction to error handling in Solidity and is intended for beginners who want to learn about the basic mechanisms for error checking and handling in smart contract development.

## Description

The ErrorHandling contract showcases:

- How to use require() for input validation.
- How to use assert() to check for invariants within the contract.
- How to use revert() for custom error handling and transaction rollback.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. Follow the steps below to compile and deploy the contract.

Open Remix IDE:
1. **Go to the Remix website at https://remix.ethereum.org/.**

2. **Create a New File:**
    - Click on the "+" icon in the left-hand sidebar.
    - Save the file with a .sol extension (e.g., ErrorHandling.sol).
    - Copy and paste the following code into the file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract ErrorHandling {
    string public contractName = "Error Handling";
    uint public storedValue;
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    // Function using require() to validate input
    function setValue(uint _value) public {
        require(_value > 0, "Value must be greater than 0");
        storedValue = _value;
    }

    // Function using assert() to check for an invariant
    function checkInvariant() public view returns (bool) {
        // Assert that storedValue is always greater than or equal to 0
        assert(storedValue >= 0);
        return true;
    }

    // Function using revert() for custom error handling
    function resetValue() public {
        if (msg.sender != owner) {
            revert("Only the owner can reset the value");
        }
        storedValue = 0;
    }

    // Function to demonstrate the combination of require, assert, and revert
    function complexFunction(uint _value) public {
        // Use require to validate initial conditions
        require(_value > 0, "Value must be greater than 0");
        require(msg.sender == owner, "Only the owner can call this function");

        // Perform some operation
        storedValue = _value * 2;

        // Use assert to check for an invariant
        assert(storedValue > _value);

        // Custom error handling using revert
        if (storedValue < _value) {
            revert("Stored value is less than the input value");
        }
    }
}

```

3. **Compile the Code:**
   - Click on the "Solidity Compiler" tab in the left-hand sidebar.
   - Make sure the "Compiler" option is set to 0.8.17 (or another compatible version).
   - Click on the "Compile ErrorHandling.sol" button.
4. **Deploy the Contract:**
   - Click on the "Deploy & Run Transactions" tab in the left-hand sidebar.
   - Select the ErrorHandling contract from the dropdown menu.
   - Click on the "Deploy" button.
     

