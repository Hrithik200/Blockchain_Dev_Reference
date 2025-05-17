# Foundry Setup and Workflow Guide

## 🚀 Getting Started with Foundry

### ✅ Step 1: Install Foundry
```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

### ✅ Step 2: Create a new Foundry project
```bash
forge init your-project-name
cd your-project-name
```

This creates the following structure:
```
your-project-name/
│
├── src/                # Place your contract here
├── script/             # Scripts for deployment/interactions
├── test/               # Unit tests go here
├── foundry.toml        # Foundry config file
```

### ✅ Step 3: Add your contract in src/
Create your Solidity contracts in the `src/` directory

### ✅ Step 4: Build your project
```bash
forge build
```

### ✅ Step 5: Write tests
Create a test file inside the `test/` directory:

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.20;

import "forge-std/Test.sol";
import "../src/MyContract.sol";

contract MyContractTest is Test {
    MyContract myContract;

    function setUp() public {
        myContract = new MyContract();
    }

    function testExample() public {
        // your test logic here
        assertEq(myContract.someValue(), 42);
    }
}
```

### ✅ Step 6: Run the tests
```bash
forge test
```

### ✅ Step 7: Format your code
```bash
forge fmt
```

### ✅ Step 8: Add dependencies (e.g., OpenZeppelin)
```bash
forge install OpenZeppelin/openzeppelin-contracts
```

## 🎯 Running Specific Tests
```bash
# Run a specific test file
forge test --match-path test/ContractName.t.sol

# Run a specific test function
forge test --match-test testName

# Run a specific test file and function
forge test --match-path test/ContractName.t.sol --match-test testName
```