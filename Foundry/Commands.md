# Solidity Development Command Reference

## 🛠️ Foundry Commands

### Core Testing Commands
```bash
# Run all tests
forge test

# Run tests with gas profiling enabled
forge test --gas-report

# Compare gas usage differences over time
forge snapshot --diff

# Inspect storage layout of a contract
forge inspect MyContract storageLayout

# Check compiled contract bytecode sizes
forge build --sizes
```

### 🔄 Anvil Commands
```bash
# Start local Ethereum node
anvil
# Output: Anvil running at http://127.0.0.1:8545
```

## 🔍 Slither Static Analysis

### Basic Usage
```bash
# Run Slither on entire project
slither .

# Run Slither on specific contract
slither contracts/MyContract.sol

# Output JSON report
slither contracts/ --json results.json

# Run specific checks
slither contracts/ --detect reentrancy
```

### Common Slither Detectors

| Detector Name         | What it checks                                                 |
| --------------------- | -------------------------------------------------------------- |
| `reentrancy`          | Detects reentrancy vulnerabilities                             |
| `uninitialized-state` | Detects uninitialized storage variables                        |
| `unused-return`       | Detects ignored return values from function calls              |
| `tx-origin`           | Detects use of `tx.origin` which is unsafe                     |
| `shadowing`           | Detects variable shadowing issues                              |
| `external-function`   | Detects external functions that could be `public` or `private` |
| `delegatecall`        | Detects use of `delegatecall` which can be dangerous           |
| `low-level-calls`     | Detects use of low-level calls like `call`, `callcode`         |
| `timestamp`           | Detects usage of `block.timestamp` which can be manipulated    |
| `dos-with-revert`     | Detects denial of service vulnerabilities with revert          |
| `unprotected-upgrade` | Detects missing access control on upgrade functions            |
| `assert`              | Detects assert statements that might fail                      |

## 💡 Testing Pro Tips

- Use `vm.assume()` to restrict invalid fuzz inputs
- Use `vm.expectRevert()` to assert failures
- Separate unit/fuzz/invariant tests in their own `.t.sol` files
- Use `forge snapshot` to monitor gas usage regressions
- Use `setUp()` for shared state setup across tests

## 🧾 Foundry CLI Reference Guide

| Command                                  | Purpose                                   |
| ---------------------------------------- | ----------------------------------------- |
| `forge test --gas-report`                | Run tests and generate a gas report       |
| `forge snapshot`                         | Save current gas report snapshot          |
| `forge snapshot --diff`                  | Compare new gas report with last snapshot |
| `forge inspect <Contract> storageLayout` | View storage layout for optimization      |
| `forge build --sizes`                    | Show contract bytecode sizes              |
