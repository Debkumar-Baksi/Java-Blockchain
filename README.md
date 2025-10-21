# NoobChain - A Simple Blockchain Implementation in Java

A proof-of-concept blockchain implementation designed to help developers understand blockchain fundamentals by building one from scratch.

## Overview

This project demonstrates core blockchain concepts including block creation, cryptographic hashing, chain validation, and proof-of-work mining. While not production-ready, it provides a solid foundation for understanding how blockchains function.

## Features

- **Block Creation**: Build blocks with digital signatures and data storage
- **Cryptographic Hashing**: SHA-256 algorithm for generating unique block fingerprints
- **Chain Validation**: Verify blockchain integrity by comparing hashes
- **Proof of Work Mining**: Mining mechanism requiring computational effort to validate blocks
- **Chain Integrity**: Tamper-evident design where any data modification breaks the chain

## Prerequisites

- Java Development Kit (JDK) installed
- IDE (Eclipse recommended) or text editor
- GSON library by Google (optional, for JSON formatting)

## Project Structure

```
noobchain/
├── NoobChain.java      # Main class with blockchain logic
├── Block.java          # Block class definition
└── StringUtil.java     # Cryptographic utility methods
```

## How It Works

### Block Structure
Each block contains:
- `hash` - The block's digital signature
- `previousHash` - Digital signature of the previous block
- `data` - Information stored in the block
- `timeStamp` - Block creation time
- `nonce` - Number used in proof-of-work mining

### Hashing Mechanism
Blocks are chained together through cryptographic hashing. Each block's hash is calculated from:
- Previous block's hash
- Block data
- Timestamp
- Nonce value

If any data in a block is modified, the hash changes, breaking the chain and making tampering evident.

### Mining (Proof of Work)
Miners must find a nonce value that produces a hash starting with a specific number of zeros. The difficulty parameter determines how many leading zeros are required.

## Getting Started

1. **Setup Project**
   ```
   File > New > Java Project
   Name: noobchain
   Create NoobChain class
   ```

2. **Add GSON Library** (Optional)
   - Download GSON from Google
   - Add to project build path

3. **Set Mining Difficulty**
   ```java
   public static int difficulty = 5;
   ```
   - Lower values (1-2): Very fast mining
   - Recommended for testing: 4-6
   - Production blockchains: Much higher (e.g., Litecoin: ~442,592)

## Usage Example

```java
// Create genesis block
Block genesisBlock = new Block("First block data", "0");
genesisBlock.mineBlock(difficulty);

// Add to blockchain
blockchain.add(genesisBlock);

// Create subsequent blocks
Block secondBlock = new Block("Second block data", genesisBlock.hash);
secondBlock.mineBlock(difficulty);
blockchain.add(secondBlock);

// Validate chain
System.out.println("Is chain valid? " + isChainValid());
```

## Chain Validation

The `isChainValid()` method ensures:
- Each block's stored hash matches its calculated hash
- Each block's `previousHash` matches the previous block's hash
- All blocks have valid mined hashes (meeting difficulty requirement)

## Security Features

**Why Blockchains Are Secure:**
- Changing data in any block changes its hash
- This breaks the chain for all subsequent blocks
- Attackers would need to re-mine all subsequent blocks
- On networks, the longest valid chain is accepted
- Attackers would need more computational power than the rest of the network combined

## Performance Notes

Mining time increases exponentially with difficulty:
- Difficulty 1-2: Nearly instant
- Difficulty 4-6: Few seconds per block
- Higher difficulties: Minutes to hours

Adjust difficulty based on your testing needs and computational resources.

## Limitations

This is a **proof-of-concept implementation** and is not production-ready. Missing features include:
- Network/peer-to-peer functionality
- Transaction handling
- Wallet system
- Consensus mechanisms beyond proof-of-work
- Merkle trees
- Security hardening

## Future Enhancements

Potential additions for learning:
- Transaction processing
- Wallet creation and management
- Network communication between nodes
- Advanced consensus algorithms
- Smart contract support

## Learning Resources

This project is part of the Blockchain Development Mega Guide and serves as an educational foundation for understanding blockchain technology.

## License

Educational/Open Source Project

## Contributing

This is a learning project. Feel free to fork, modify, and experiment with the code to deepen your blockchain understanding.

---

**Note**: For production cryptocurrency projects, consider using established frameworks and platforms rather than building from scratch.
