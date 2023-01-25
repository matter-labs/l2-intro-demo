# Intro to Layer 2s

This repository contains all the code examples used in the "Introduction to L2s" workshop.
**This project was scaffolded with [zksync-cli](https://github.com/matter-labs/zksync-cli).**

## Workshop tasks

### 1. zkSync portal and faucets

The [zkSync Portal](https://portal.zksync.io/) is the easiest way to deposit and withdraw funds from zkSync. If you have GoerliETH, you can use the [bridge section](https://portal.zksync.io/bridge) to deposit or withdraw funds to and from the zkSync testnet.

However, if you don't have any GoerliETH, you can receive a small amount by using our [faucet](https://portal.zksync.io/faucet), which requires you to post a tweet as a way to verify your identity.

On the other hand, here are a few other faucets that you can use:

- https://goerlifaucet.com/
- https://goerli-faucet.pk910.de/

### 2. Create a project with zksync-cli

The zkSync CLI tool is the easiest way to start developing applications and smart contracts on zkSync. To install it, just run `npm i -g zksync-cli@latest`.

Currently, the zksync-cli provides three methods: deposit, withdraw and create.

To create a new project, just run `zksync-cli create NAME_OF__YOUR_PROJECT`. This will create a new folder with the project name and create a sample project inside it.

It's very similar to any other Hardhat project, but the `hardhat.config.ts` file includes some zkSync-specific properties.

First, it imports a few dependencies used to compile and deploy our contracts:

```typescript
//
import "@matterlabs/hardhat-zksync-deploy";
import "@matterlabs/hardhat-zksync-solc";
```

Secondly, it includes the `zksolc` object which contains the properties of the compiler. Learn more about the [zksolc configuration here](https://v2-docs.zksync.io/api/hardhat/plugins.html#hardhat-zksync-solc).

An last, the networks are defined with the following parameters:

```js
  url: "https://zksync2-testnet.zksync.dev",
  ethNetwork: "goerli",
  zksync: true,
```

The `url` and `ethNetwork` are the RPC endpoints of the L2 and L1 and the `zksync` flag is used to indicate Hardhat if it should use the zksync compiler.

### 3. Deploy and interact with the `Greeter` contract

The zkSync-CLI sample project includes a `Greeter` contract and a deploy script. The greeter contract stores a message on chain which can be retrieved by calling the read method `greet()` and can be updated by calling the method `setGreeting(_message)`.

To compile the contract, run `yarn hardhat compile`. You'll notice that the folders `artifacts-zk` and `cache-zk` will be created. The

To deploy the contract, just set your wallet's private key in the `.env` file (you'll have to rename it first), and run the command `yarn hardhat deploy-zksync --script deploy-greeter.ts`

### 4. Create and deploy an ERC20 contract

To showcase the compatibility with standards, we'll use the [OpenZeppeling contract wizard](https://wizard.openzeppelin.com/#erc20) to create an ERC20 contract. We'll choose an ERC20, Burnable, Pausable. We can take the contract and put it in the `contracts` folder as is (check out file [zkToken.sol](./contracts/zkToken.sol)). To compile the contract, we just have to run `yarn hardhat compile`.

### 5. Create and deploy an ERC721 contract

To showcase the compatibility with standards, we'll use the [OpenZeppeling contract wizard](https://wizard.openzeppelin.com/#erc20) to create an ERC721 contract.

## POAP NFTs

To receive a POAP NFT for completing these tasks, you need to follow the intructions mentioned during the workshop.

## Project structure

Projects created with the zkSync-CLI have the following structure.

- `/contracts`: smart contracts.
- `/deploy`: deployment and contract interaction scripts.
- `/test`: test files
- `hardhat.config.ts`: configuration file.

## Commands

- `yarn hardhat compile` will compile the contracts.
- `yarn run deploy` will execute the deployment script `/deploy/deploy-greeter.ts`. Requires [environment variable setup](#environment-variables).
- `yarn run greet` will execute the script `/deploy/use-greeter.ts` which interacts with the Greeter contract deployed.
- `yarn test`: run tests. **Check test requirements below.**

Both `yarn run deploy` and `yarn run greet` are configured in the `package.json` file and run `yarn hardhat deploy-zksync`.

### Environment variables

In order to prevent users to leak private keys, this project includes the `dotenv` package which is used to load environment variables. It's used to load the wallet private key, required to run the deploy script.

To use it, rename `.env.example` to `.env` and enter your private key.

```
WALLET_PRIVATE_KEY=123cde574ccff....
```

### Local testing

In order to run test, you need to start the zkSync local environment. Please check [this section of the docs](https://v2-docs.zksync.io/api/hardhat/testing.html#prerequisites) which contains all the details.

If you do not start the zkSync local environment, the tests will fail with error `Error: could not detect network (event="noNetwork", code=NETWORK_ERROR, version=providers/5.7.2)`

## Official Links

- [Website](https://zksync.io/)
- [Documentation](https://v2-docs.zksync.io/dev/)
- [GitHub](https://github.com/matter-labs)
- [Twitter](https://twitter.com/zksync)
- [Discord](https://discord.gg/nMaPGrDDwk)
