# DeFi on Stellar

A project exploring decentralized finance (DeFi) applications on the Stellar blockchain. This repository provides tools and smart contract implementations to enable seamless financial operations, including token swaps, lending, and borrowing, on Stellar's fast and scalable network.

## Features

- **Token Swaps**: Efficiently exchange assets on the Stellar network.
- **Lending and Borrowing**: Implement financial primitives to lend and borrow assets.
- **Stellar Ecosystem Integration**: Leverage Stellar's unique features, including low fees and fast transactions.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v16.x or higher)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- Stellar SDK for JavaScript

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/rajeebkm/defi-on-stellar.git
   cd defi-on-stellar
   ```

2. Install dependencies:
   ```bash
   npm install
   # or
   yarn install
   ```

3. Set up environment variables:
   Create a `.env` file in the root directory and configure the following:
   ```env
   STELLAR_NETWORK=<testnet or public>
   SECRET_KEY=<your-stellar-secret-key>
   ```

### Usage

1. Run the application:
   ```bash
   npm start
   ```

2. Test the functionality:
   Run unit tests to ensure everything works as expected:
   ```bash
   npm test
   ```

## Project Structure

- `src/`: Core application logic for DeFi operations.
- `contracts/`: Smart contracts for DeFi operations on Stellar.
- `scripts/`: Utilities and deployment scripts.
- `test/`: Unit tests to ensure robust functionality.

## Example

Below is an example of initiating a token swap:

```javascript
const StellarSdk = require("stellar-sdk");

async function swapTokens() {
    const server = new StellarSdk.Server("https://horizon-testnet.stellar.org");
    const sourceKeys = StellarSdk.Keypair.fromSecret("<your-secret-key>");
    const transaction = new StellarSdk.TransactionBuilder(
        await server.loadAccount(sourceKeys.publicKey()),
        { fee: StellarSdk.BASE_FEE, networkPassphrase: StellarSdk.Networks.TESTNET }
    )
        .addOperation(
            StellarSdk.Operation.manageSellOffer({
                selling: new StellarSdk.Asset("TOKEN1", "IssuerPublicKey"),
                buying: StellarSdk.Asset.native(),
                amount: "100",
                price: "0.5",
            })
        )
        .setTimeout(30)
        .build();

    transaction.sign(sourceKeys);
    await server.submitTransaction(transaction);
    console.log("Token swap successful!");
}

swapTokens().catch(console.error);
```

## Contributing

Contributions are welcome! Fork this repository and submit a pull request for any enhancements or fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/rajeebkm/defi-on-stellar/blob/main/LICENSE) file for details.

## Acknowledgements

- [Stellar Developers](https://developers.stellar.org/) for comprehensive documentation and support.
- [rajeebkm](https://github.com/rajeebkm) for initiating and maintaining this project.
