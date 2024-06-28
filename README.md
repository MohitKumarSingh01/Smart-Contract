# LoanEligibility Contract

## Overview

The `LoanEligibility` contract is a smart contract deployed on the Ethereum blockchain. It allows the owner to check the eligibility of a user for different types of loans based on their credit score. The contract provides functionalities to verify credit score requirements for Home Loans, Car Loans, Personal Loans, and a general minimum credit score requirement.

## Features

- Check eligibility for different types of loans based on credit score.
- Emit events when the credit score is updated.
- Only the contract owner can perform credit score checks and updates.
- Use of `require`, `assert`, and `revert` statements to enforce credit score requirements.

## Functions

### Constructor

- `constructor()`
  - Sets the contract deployer as the owner.

### Public Functions

- `checkForHomeLoan(uint256 currentCreditScore)`
  - Checks if the given credit score is eligible for a Home Loan.
  - Requirements:
    - Credit score must be above 750.
  - Emits `creditScoreChanged` event.

- `checkForCarLoan(uint256 currentCreditScore)`
  - Checks if the given credit score is eligible for a Car Loan.
  - Requirements:
    - Credit score must be above 650.
  - Emits `creditScoreChanged` event.

- `checkForPersonalLoan(uint256 currentCreditScore)`
  - Checks if the given credit score is eligible for a Personal Loan.
  - Requirements:
    - Credit score must be above 550.
  - Emits `creditScoreChanged` event.

- `checkMinimumCreditScore()`
  - Asserts that the current credit score is at least 300.
  - Note: Assert statements do not provide error messages.

- `checkForAnyLoan(uint256 currentCreditScore)`
  - Checks if the given credit score is eligible for any loan.
  - Requirements:
    - Credit score must be above 500.
  - Emits `creditScoreChanged` event.

## Events

- `creditScoreChanged(uint256 currentCreditScore)`
  - Emitted when the credit score is updated.

## Modifiers

- `onlyOwner`
  - Restricts access to the owner of the contract.

## Usage

1. Deploy the contract to the Ethereum network.
2. Only the owner of the contract can invoke the credit score check functions.
3. The functions will validate the provided credit score and update the contract's state if the credit score meets the eligibility requirements.

## Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract LoanEligibility 
{
    uint256 public creditScore = 500;
    address public owner;

    // Event to modify old credit score by current credit score
    event creditScoreChanged(uint256 currentCreditScore);

    // Modifier to restrict access to the owner
    modifier onlyOwner() 
    {
        require(msg.sender == owner, "Caller is not the owner");
        _;
    }

    constructor() 
    {
        // Set the contract deployer as the owner
        owner = msg.sender;
    }

    // Function to check eligibility for Home Loan
    function checkForHomeLoan(uint256 currentCreditScore) external onlyOwner 
    {
        require(currentCreditScore > 750, "You are not eligible for a Home Loan. Your credit score must be above 750.");

        creditScore = currentCreditScore;
        emit creditScoreChanged(currentCreditScore);
    }

    // Function to check eligibility for Car Loan
    function checkForCarLoan(uint256 currentCreditScore) external onlyOwner 
    {
        require(currentCreditScore > 650, "You are not eligible for a Car Loan. Your credit score must be above 650.");

        creditScore = currentCreditScore;
        emit creditScoreChanged(currentCreditScore);
    }

    // Function to check eligibility for Personal Loan
    function checkForPersonalLoan(uint256 currentCreditScore) external onlyOwner
    {
        require(currentCreditScore > 550, "You are not eligible for a Personal Loan. Your credit score must be above 550.");

        creditScore = currentCreditScore;
        emit creditScoreChanged(currentCreditScore);
    }

    // Function that uses assert statement for getting minimum credit score
    function checkMinimumCreditScore() external view 
    {
        assert(creditScore >= 300); // This should always be true
        // Note: Assert statements do not provide error messages, so no additional message is given here.
    }

    // Function to demonstrate revert statement to check eligibility for any loan
    function checkForAnyLoan(uint256 currentCreditScore) external onlyOwner 
    {
        if (currentCreditScore <= 500) {
            revert("You do not have the minimum credit score for any loan. Your credit score must be above 500.");
        }
        creditScore = currentCreditScore;
        emit creditScoreChanged(currentCreditScore);
    }
}
```

## License

This project is licensed under the MIT License.
