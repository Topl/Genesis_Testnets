# Genesis (Testnets)
This repository contains data files which encode "genesis" blocks for Topl's testnets.  A "genesis" block (a.k.a. "big bang" block) is the first block in a blockchain.  In particular, it contains the initial distribution of tokens and staking registrations for the network.

## Structure
Unlike the Topl "Mainnet", there may be many Topl "Testnets", especially as we iterate and improve upon the technology.  As such, this repository contains a sub-directory for each unique testnet blockchain that is launched.  A testnet may conclude if a breaking change is implemented in the protocol, and a fork would need to be avoided.  For example, this repository may be structured like:
- `README.md`
- `testnet0/`
- `testnet1/`
- `testnet2/`
- ...

### Genesis structure
Within each testnet directory, a genesis block is encoded using protobuf in a normalized structure.  The contents should include:
- `{blockId}.header.pbuf`
  - A protobuf-encoded BlockHeader file, where `{blockId}` is the ID of the genesis block
- `{blockId}.body.pbuf`
  - A protobuf-encoded BlockBody file, where `{blockId}` is the ID of the genesis block
  - From the decoded BlockBody, the transactionIds can be extracted which should map to the following files
- `{transactionId0}.transaction.pbuf`
  - A protobuf-encoded IoTransaction file, where `{transactionId0}` is the ID of the transaction contained within the genesis block
- `{transactionId1}.transaction.pbuf`
- `{transactionId2}.transaction.pbuf`
- ...
- `{transactionIdN}.transaction.pbuf`

#### Creation
A testnet genesis block can be created using the Bifrost CLI (not yet implemented at this time).  The CLI will output the files that should be uploaded (via Pull Request) to this repository.

## Node Launch
A Bifrost node can be configured to point to this repository for its genesis configuration.  The custom configuration would include:
```yaml
bifrost:
  bigBang:
    type: public
    genesisBlockId: b_abcd123
    sourcePath: https://raw.githubusercontent.com/Topl/Genesis_Testnets/main/testnet5/
```
