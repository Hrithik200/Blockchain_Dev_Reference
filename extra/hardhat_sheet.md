# Hardhat Cheat Sheet

> A concise guide for setting up, using, and debugging smart contracts using Hardhat.

---

## ✅ 1. Install Hardhat

### Initialize a new project:

```bash
mkdir my-hardhat-project
cd my-hardhat-project
npm init -y
npm install --save-dev hardhat
```

### Create boilerplate project:

```bash
npx hardhat
```

Choose `Create a basic sample project` and install dependencies.

---

## ✅ 2. Common Hardhat Commands

| Command                       | Purpose                                |
| ----------------------------- | -------------------------------------- |
| `npx hardhat compile`         | Compile all contracts                  |
| `npx hardhat test`            | Run test cases in `test/` folder       |
| `npx hardhat run scripts/...` | Run a script (e.g., deploy.js)         |
| `npx hardhat node`            | Start a local Hardhat node             |
| `npx hardhat console`         | Launch interactive Solidity/JS console |
| `npx hardhat clean`           | Clear build cache and artifacts        |
| `npx hardhat accounts`        | Print dev accounts                     |
| `npx hardhat help`            | View all available Hardhat commands    |

---

## ✅ 3. Using `console.log` in Solidity

### Add to your contract:

```solidity
import "hardhat/console.sol";

contract Demo {
    uint256 public count;

    function increment() public {
        count++;
        console.log("Count is now", count);
    }
}
```

### Other console helpers:

```solidity
console.log("Address:", msg.sender);
console.logBytes32(keccak256("value"));
console.logBool(true);
```

> Works in tests or local scripts only. Not available on mainnet or other live chains.

---

## ✅ 4. Example Deployment Script

Create `scripts/deploy.js`:

```js
async function main() {
  const [deployer] = await ethers.getSigners();
  console.log("Deploying with:", deployer.address);

  const Token = await ethers.getContractFactory("MyToken");
  const token = await Token.deploy();

  console.log("Token deployed to:", token.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

Run with:

```bash
npx hardhat run scripts/deploy.js --network localhost
```

---

## ✅ 5. Run Tests

```bash
npx hardhat test
```

Supports Mocha, Chai, Ethers.js, Waffle.

---



## ✅ 6. Optional: Enable TypeScript

```bash
npm install --save-dev typescript ts-node @types/node
npx hardhat
```

Choose TypeScript when prompted.

---

