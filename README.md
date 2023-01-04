![created by Supercolony](https://supercolony.net/img/new-logo-horizontal-green-white.svg)

## Overview :page_facing_up:

Typechain was created by [Supercolony](https://supercolony.net/) and is maintained by [Brushfam] to to improve developers’ experience working with ink! smartcontracts.

Nowadays, when technologies are growing faster and faster, we should think about optimizations of different routine processes and making older stuff better. One of these optimizations is to make code typesafe that will be flexible in different situations.

When a smart contract is being written, front-end developer receives file representation of it in the format called Application Binary Interface (ABI). One ABI per each contract, new ABI for every update of a contract.

Information about how to interact with a contract (methods names, arguments & returns types etc.) is included in this ABI file. It is not quite human-readable, so extraction of that information becomes a challenge. We need to have correct type definitions for each contract in TypeScript.

Interaction with blockchain is done with polkadot.js library, which only has abstract definitions for the contract in use, thus users' code cannot be typesafe. And Typechain-Polkadot can change it.

### Installation & import

Install the package as dependency:

```bash
npm i @727-ventures/typechain-polkadot
```

Pass the folder with artifacts(in the example it is `artifacts`) as input argument
and the output folder(in the example it is `typed_contracts`):
```bash
npx @727-ventures/typechain-polkadot --in artifacts --out typed_contracts
```

Import the contract what you want to use(in the example it is [`my_psp22`](https://github.com/727-Ventures/openbrush-contracts/tree/main/examples/psp22)):
```typescript
import MyPSP22 from "../typed_contracts/contracts/my_psp22"
```

In the code you can find all available methods and constructors.

Right now, you can't instantiate the contract via typechain(coming soon),
but you can wrap any already deployed contract. If in the code you already
have instantiated `contract` then you can easily wrap it:

```typescript
const typed_contract = new MyPSP22(
    contract.address.toString(),
    signer /* who will sign transactions*/,
    contract.api
);
```

More information you can find in [docs](docs/about.md).

### Usage of Typechain-compiler

```bash
npx typechain-compiler --config config.json
```

Also you can set some additional arguments like `--noCompile`, `--noTypechain`, `--release`

Config interface will be something like this:
```typescript
export interface Config {
    projectFiles: string[]; // Path to all project files, everystring in glob format
    skipLinting : boolean; // Skip linting of project files
    artifactsPath : string; // Path to artifacts folder, where artifacts will be stored it will save both .contract and .json (contract ABI)
    typechainGeneratedPath : string; // Path to typechain generated folder
}
```

### Project Details

Typesafe contracts' descriptions can be generated automatically by a script, taking a list of ABIs as an input, giving usable TS type definitions and even runtime code as its output.

Given, that a front-end developer needs to do this with every contracts update, such tool would save a lot of time and prevent mistakes of misusing smart contracts. It is installed as a package with built-in CLI.

When contracts descriptions come both with ABI and source code (`*.contract` files), our tool will provide means for deployment as well.

Also, Typechain-Polkadot uses awesome tool Handlebars for generating code from templates. It is a very flexible and powerful tool, which allows to generate code from templates with a lot of different logic.
For example, you can generate code for different contracts with different logic, or you can generate code for different methods with different logic.

## Roadmap 🚗

Typechain participates in the Web3 Grants, you can find the roadmap there:
- [Grant I](https://github.com/w3f/Grants-Program/blob/master/applications/typechain-polkadot.md)
  - [Delivery milestone 1](https://github.com/w3f/Grant-Milestone-Delivery/blob/master/deliveries/typechain-polkadot-milestone-1.md#milestone-delivery-mailbox)
- Grant II - Comming soon....

### Our Element Chat

If you have any questions regarding Typechain-Polkadot, you can join the [Brushfam Element channel](https://matrix.to/#/!utTuYglskDvqRRMQta:matrix.org?via=matrix.org&via=t2bot.io&via=web3.foundation) to find your answers and meet other ink! smart contracts developers.

-----------
#### Made with ❤️ by [Supercolony](https://supercolony.net/)
