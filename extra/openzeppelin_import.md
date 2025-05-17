# To import any openzeppelin Library into your contact  
````bash
Visit https://github.com/OpenZeppelin/openzeppelin-contracts
Move to your preferred contact page
copy the path that is showing


````
For Remix/ide
```bash
step 1 :https://github.com/OpenZeppelin/openzeppelin-contracts
Step 2 : want to get path for erc20 so bon this page 
 https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol

 copy this contracts/token/ERC20/ERC20.sol

 and use @openzepplin prefix in solidity
````


 For Foundry
```bash
To Install OpenZeppelin Contracts

forge install OpenZeppelin/openzeppelin-contracts

This clones the GitHub repo into lib/openzeppelin-contracts/.

🔹 Then  Import in Your Solidity Files
Use relative-style imports (preferred in Foundry):
import "openzeppelin-contracts/contracts/token/ERC20/extensions/ERC4626.sol";
✅ This works because:

lib/openzeppelin-contracts is aliased as openzeppelin-contracts/ by Foundry automatically via remappings.txt.
````
