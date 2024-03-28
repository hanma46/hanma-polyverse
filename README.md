# PIT Phase 2 repo project: Cross-chain Proof of NFT

This repository is created to enter the PIT phase 2.

## Team Members

- @nam65678

## Description

This application enables a user to submit a vote a ballot on a contract on OP Sepolia. The information about this vote subsequently gets sent to an ERC721 NFT contract on Base Sepolia to mint an NFT related to the vote.

Features:

- Uses Polymer x IBC as the cross-chain format
- Commits to the spirit of application specific chains/rollups where voting functionality could be specialized on one chain, NFT marketplace on another and both can form composable applications through interoperability.

## Resources used

The repo uses the [ibc-app-solidity-template](https://github.com/open-ibc/ibc-app-solidity-template) as starting point and adds custom contracts XBallot and XProofOfVoteNFT that implement the custom logic.

It changes the send-packet.js script slightly to adjust to the custom logic.

The expected behaviour from the template should still work but nevertheless we quickly review the steps for the user to test the application...
Run `just --list` for a full overview of the just commands.

Additional resources used:
- Hardhat
- Blockscout
- Tenderly

## Steps to reproduce

After cloning the repo, install dependencies:

```sh
just install
```

And add your private key to the .env file (rename it from .env.example).

### Sending a packet

Now with an existing channel in the config (your own or the default), run:

```sh
just do-it
```
You'll see an active waiting poll in the terminal and will be informed if the packet was sent successfully.

## Proof of testnet interaction

After following the steps above you should have interacted with the testnet. You can check this at the [IBC Explorer](https://sepolia.polymer.zone/packets).

Here's the data of our application:

- XBallot (OP Sepolia) : 0x5C3F52f83544Aa625F57Fa674080Ce017920857d
- XProofOfVoteNFT (Base Sepolia): 0x2db37cbbbd4795cf6b4015af2c35383539d76ead
- Channel (OP Sepolia): channel-39838
- Channel (Base Sepolia): channel-39839

- Proof of Testnet interaction:
    - [SendTx](https://optimism-sepolia.blockscout.com/tx/0xac9837010f0f58f0d39c03bb4a94055e790e4ed59f7b5edfcd4e5ea3f6e4707f)
    - [RecvTx](https://base-sepolia.blockscout.com/tx/0x0c4704543223c8451285d590dbc530ff885c7b0a39b6a1bd8a39dfaba44c3fb1)
    - [Ack](https://optimism-sepolia.blockscout.com/tx/0x466998984a225844e6a808419b2f945859f1407b90d70240bb3b2f111328875e)

## Challenges Faced

- Debugging used to be tricky when the sendPacket on the contract was successfully submitted but there was an error further down the packet lifecycle.
What helped was to verify the contracts and use Tenderly for step-by-step debugging to see what the relayers submitted to the dispatcher etc.

## What we learned

How to make the first dApp using Polymer.

## Future improvements

Basic functionality was implemented, but the following things can be improved:

- More tests
- More input validation
- Add event listeners related to important IBC lifecycle steps

## Licence

[Apache 2.0](LICENSE)
