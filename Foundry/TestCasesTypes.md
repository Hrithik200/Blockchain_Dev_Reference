# Smart Contract Testing Strategy Guide

## 🧪 Types of Tests for Smart Contracts

| Test Type | Description | Common Tools |
|-----------|-------------|--------------|
| **Unit Tests** | Test individual functions in isolation | Foundry, Hardhat |
| **Negative Tests** | Verify functions revert with expected errors | `vm.expectRevert()` |
| **Fuzzing** | Auto-generate random inputs to find edge cases | Foundry fuzzing |
| **Invariants** | Verify properties that should always remain true | Foundry invariant tests |
| **Access Control** | Validate permission systems work correctly | Role-based testing |
| **Edge Case Tests** | Test boundary conditions and limits | Min/max values |
| **Event Emission** | Verify events are emitted with correct parameters | `vm.expectEmit()` |
| **Gas Profiling** | Analyze and optimize gas consumption | `--gas-report` |
| **Reentrancy/Custom Logic** | Test for complex vulnerabilities | Mocks and attack contracts |

## 📋 Categories of Test Cases

### 1. Happy Path (Positive Tests)
**Purpose:** Verify functions work correctly with valid inputs under normal conditions.

**Examples:**
- Token minting succeeds with proper permissions
- Deposits credit the correct account
- Withdrawals transfer the right amount
- Standard transfers work as expected

### 2. Edge Cases
**Purpose:** Test at boundaries and limits where bugs often hide.

**Examples:**
- Mint exactly at max supply
- Transfer total balance (not partial)
- Interact with zero addresses
- Use maximum/minimum allowed values
- Empty arrays or strings
- First transaction after initialization
- Actions affecting multiple accounts simultaneously

### 3. Negative Tests (Failure & Reverts)
**Purpose:** Verify functions fail appropriately with invalid inputs.

**Examples:**
- Unauthorized access attempts
- Out-of-bounds operations
- Insufficient balances
- Impossible state transitions
- Function calls in incorrect order
- Reentrancy attempts

### 4. State Transitions
**Purpose:** Confirm internal state changes correctly after operations.

**Examples:**
- Balance updates after transfers
- Counter increments
- Status flags change appropriately
- Mapping updates correctly

### 5. Events
**Purpose:** Verify correct events are emitted with accurate parameters.

**Examples:**
- Transfer events include from, to, and amount
- State change events with old and new values
- Administrative action events with actor address

### 6. Access Control
**Purpose:** Validate permission systems prevent unauthorized actions.

**Examples:**
- Owner-only functions rejected for non-owners
- Role-based permissions work correctly
- Timelock restrictions enforced
- Multi-signature requirements upheld

## 🔄 Testing Workflow Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "forge-std/Test.sol";
import "../src/Token.sol";

contract TokenTest is Test {
    Token token;
    address owner = address(1);
    address user = address(2);
    
    function setUp() public {
        vm.startPrank(owner);
        token = new Token("Test", "TST");
        token.grantRole(token.MINTER_ROLE(), owner);
        vm.stopPrank();
    }
    
    // Happy Path
    function testMint() public {
        vm.prank(owner);
        token.mint(user, 100);
        assertEq(token.balanceOf(user), 100);
    }
    
    // Edge Case
    function testMintMaxSupply() public {
        vm.startPrank(owner);
        // Mint up to the limit
        token.mint(user, token.MAX_SUPPLY());
        
        // Try to mint one more - should fail
        vm.expectRevert("Exceeds max supply");
        token.mint(user, 1);
        vm.stopPrank();
    }
    
    // Negative Test
    function testUnauthorizedMint() public {
        vm.prank(user); // user doesn't have MINTER_ROLE
        vm.expectRevert("AccessControl: account lacks role");
        token.mint(user, 100);
    }
    
    // Event Test
    function testMintEvent() public {
        vm.expectEmit(true, true, true, true);
        emit Transfer(address(0), user, 100);
        
        vm.prank(owner);
        token.mint(user, 100);
    }
}
```