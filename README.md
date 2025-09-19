# Merkle Airdrop

A Solidity smart contract implementation for distributing ERC20 tokens using Merkle trees and cryptographic signatures. This project demonstrates an efficient and secure way to conduct airdrops to multiple recipients while minimizing gas costs and preventing unauthorized claims.

## 🚨 Security Warning

**This project is for educational purposes only.** The private keys and addresses used in this codebase are publicly known test keys and should **NEVER** be used with real money or on mainnet. Always use your own secure private keys and proper key management practices in production environments.

## Features

- **Merkle Tree Verification**: Uses Merkle proofs to verify eligible recipients without storing all addresses on-chain
- **EIP-712 Signatures**: Implements typed structured data signing for enhanced security
- **Gas Efficient**: Minimizes on-chain storage by using Merkle trees
- **Replay Protection**: Prevents double-claiming through signature verification and claim tracking
- **zkSync Compatibility**: Includes deployment scripts for zkSync Era

## Project Structure

```
├── src/
│   ├── MerkleAirdrop.sol    # Main airdrop contract
│   └── BagelToken.sol       # Example ERC20 token for testing
├── script/
│   ├── DeployMerkleAirdrop.s.sol  # Deployment script
│   ├── GenerateInput.s.sol        # Generate merkle tree input
│   ├── MakeMerkle.s.sol           # Create merkle tree and proofs
│   └── Interact.s.sol             # Interaction scripts
├── test/
│   └── MerkleAirdrop.t.sol        # Test suite
└── Makefile                       # Build and deployment commands
```

## How It Works

1. **Merkle Tree Generation**: A list of eligible addresses and amounts is converted into a Merkle tree
2. **Root Storage**: Only the Merkle root is stored on-chain, saving gas
3. **Claim Process**: Users provide their allocation amount, Merkle proof, and a signature
4. **Verification**: The contract verifies:
   - The Merkle proof against the stored root
   - The signature matches the claiming address
   - The address hasn't already claimed

## Smart Contract Features

### MerkleAirdrop.sol

- `claim()`: Main function for users to claim their tokens
- `getMessageHash()`: Returns the hash for EIP-712 signature verification
- Built-in replay protection and signature validation
- Inherits from OpenZeppelin's EIP712 for standardized signature handling

### BagelToken.sol

- Standard ERC20 token used for testing
- Mintable by owner for demonstration purposes

## Getting Started

### Prerequisites

- [Foundry](https://getfoundry.sh/) installed
- Node.js (for zkSync CLI)

### Installation

```bash
git clone <repository-url>
cd merkle-airdrop
make install
```

### Building

```bash
make build
```

### Testing

```bash
make test
```

## Usage

### Local Development

1. **Start local blockchain**:

   ```bash
   make anvil
   ```

2. **Generate Merkle tree data**:

   ```bash
   make merkle
   ```

3. **Deploy contracts**:

   ```bash
   make deploy
   ```

4. **Claim tokens**:
   ```bash
   make claim
   ```

### zkSync Development

1. **Start zkSync local node**:

   ```bash
   make zk-anvil
   ```

2. **Deploy to zkSync**:
   ```bash
   make deploy-zk
   ```

## Available Make Commands

- `make build` - Compile contracts
- `make test` - Run test suite
- `make deploy` - Deploy to local Anvil
- `make deploy-zk` - Deploy to zkSync local
- `make merkle` - Generate Merkle tree and proofs
- `make claim` - Execute a test claim
- `make balance` - Check token balance
- `make anvil` - Start local Ethereum node
- `make zk-anvil` - Start zkSync local node

## Configuration

The Makefile contains several configuration constants:

- **Test Addresses**: Pre-configured Anvil test addresses
- **zkSync Keys**: Test keys for zkSync development
- **Merkle Data**: Example root and proofs for testing

## Testing

The test suite covers:

- Successful token claims
- Merkle proof verification
- Signature validation
- Replay attack prevention
- Error conditions and edge cases

Run with:

```bash
forge test -vv
```

## Deployment Networks

- **Local Anvil**: Default development environment
- **zkSync Local**: Local zkSync Era node
- **Sepolia**: Ethereum testnet (configure with environment variables)
- **zkSync Sepolia**: zkSync Era testnet

## Important Notes

- This is a learning project and should not be used in production without thorough security audits
- Private keys in this repository are test keys only
- Always verify contracts before deploying to mainnet
- Consider gas optimizations for large-scale airdrops

## Contributing

This project is for educational purposes. Feel free to fork and experiment, but remember to never use the included private keys with real funds.

## Educational Value

This project demonstrates:

- Merkle tree implementation in Solidity
- EIP-712 signature standards
- Gas-efficient smart contract design
- Cross-chain deployment (Ethereum vs zkSync)
- Foundry development workflow
- Security best practices in smart contracts
