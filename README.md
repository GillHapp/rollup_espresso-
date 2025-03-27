# Arbitrum Nitro Rollup & Espresso Integration

This repository contains the smart contract code powering Arbitrum Nitro and Espresso integration. It includes the rollup contracts, fraud proof mechanisms, and interfaces for interacting with precompiles.

---

## Table of Contents  
1. [Getting Started](#getting-started)  
   - [Prerequisites](#prerequisites)  
   - [Setup](#setup)  
2. [Deploying Contracts to Sepolia](#deploying-contracts-to-sepolia)  
   - [Step 1: Compile Contracts](#step-1-compile-contracts)  
   - [Step 2: Set Up Environment Variables](#step-2-set-up-environment-variables)  
   - [Step 3: Deploy Rollup Creator and Initialize Espresso Contracts](#step-3-deploy-rollup-creator-and-initialize-espresso-contracts)  
   - [Step 4: Create the Rollup](#step-4-create-the-rollup)  
3. [Deployed Contract Addresses](#deployed-contract-addresses)  
4. [License](#license)  

---

## Getting Started  

### Prerequisites  
Before proceeding, ensure you have the following installed on your machine:  
- [Node.js](https://nodejs.org/) (v16 or later)  
- [Yarn](https://yarnpkg.com/)  
- [Foundry](https://book.getfoundry.sh/) for Solidity development  
- [Hardhat](https://hardhat.org/)  

### Setup  
1. **Clone the repository**  
   ```bash  
   git clone https://github.com/GillHapp/rollup_espresso-  
   cd rollup_espresso-  
   ```  
2. **Install dependencies and build the project**  
   ```bash  
   yarn install  
   yarn build  
   yarn build:forge  
   ```  

---

## Deploying Contracts to Sepolia  

### Step 1: Compile Contracts  
Run the following commands to compile the contracts locally:  
```bash  
yarn build  
yarn build:forge  
```  

### Step 2: Set Up Environment Variables  
1. Copy the sample environment file:  
   ```bash  
   cp .env.sample.goerli .env  
   ```  
2. Open the `.env` file and fill in the following values:  
   - **Etherscan API Key:** [Obtain it here](https://docs.etherscan.io/getting-started/viewing-api-usage-statistics).  
   - **Infura API Key:** [Create API here](https://docs.infura.io/dashboard/create-api).  
   - **Private Key:** Add a private key with some funds on the Sepolia network.  
   
   This key will be used to deploy the rollup contracts.  

3. **ROLLUP_CREATOR_ADDRESS:**  
   - If you want to use an already deployed `RollupCreator`, update this address in the `espresso-deployments/sepolia.json` file.  
   - Otherwise, leave it empty and follow Step 3 to deploy your own.  

### Step 3: Deploy Rollup Creator and Initialize Espresso Contracts  
To deploy the rollup creator and initialize Espresso contracts, run:  
```bash  
npx hardhat run scripts/deployment.ts --network sepolia  
```  

### Step 4: Create the Rollup  
1. Rename `config.ts.example` to `config.ts`:  
   ```bash  
   mv config.ts.example config.ts  
   ```  
2. Update the rollup-specific configurations in the `config.ts` file.  
3. Run the following command to create the rollup:  
   ```bash  
   npx hardhat run scripts/createEthRollup.ts --network sepolia  
   ```  

---

## Deployed Contract Addresses  
Once the deployment is successful, the following contracts will be created and verified on Sepolia:  

```
Calling createRollup to generate a new rollup ...  
Congratulations! 🎉🎉🎉 All DONE! Here's your addresses:  

- **RollupProxy Contract:** `0xFfc94Fd608b26d4D1aC768d75BB27722483B0766`  
- **Inbox (proxy) Contract:** `0xCEf542bD9E5c52Ebcf881E70a4229e4e2e02531F`  
- **Outbox (proxy) Contract:** `0x6b49F3B7b9971f1634222211decfcd048A79F4dC`  
- **rollupEventInbox (proxy) Contract:** `0xc4518Ad364E8d9FbE53CE81E5cba11051b463e38`  
- **challengeManager (proxy) Contract:** `0xb7EB5f4A51DdCa63609BC8F015a5739B772E8cE9`  
- **AdminProxy Contract:** `0x6a04b25c88Cb10950EBc2C3cF81E7C3c0C0f75F5`  
- **SequencerInbox (proxy) Contract:** `0x530444cd79339418dD9B64A7662b0A83f71f2c0E`  
- **Bridge (proxy) Contract:** `0x10edA64FAF0BB452771776Af8beAb703fe44020B`  
- **ValidatorUtils Contract:** `0x919059e744bF9A0EBA78678b7B5E7db4AA02a370`  
- **ValidatorWalletCreator Contract:** `0x166CFb12E3E0D1028a5257E04cEd709C7cf1b736`  

All contracts were deployed at **block number: 135345138**.  

The RollupProxy contract has been verified on the block explorer.  

---

## License  

Nitro is currently licensed under a [Business Source License](./LICENSE.md), similar to Uniswap and Aave, with an **Additional Use Grant**.  

This grant ensures users can run nodes on public Arbitrum chains without restrictions and deploy the Nitro software in a permissionless, cost-free manner if the chain settles to Arbitrum One or Arbitrum Nova.  

### Arbitrum Expansion Program (AEP)  
For deployments on Ethereum (L2) or other Layer-2 solutions, the [Arbitrum Expansion Program (AEP)](https://docs.arbitrum.foundation/assets/files/Arbitrum%20Expansion%20Program%20Jan182024-4f08b0c2cb476a55dc153380fa3e64b0.pdf) permits permissionless deployment, with a requirement to contribute **10% of net revenue** back to the Arbitrum community.  

---

For more details, check the [espresso-deployments folder](./espresso-deployments/). Happy building! 🚀
