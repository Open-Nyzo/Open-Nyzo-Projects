# Wallet servers

Wallet servers - Also known as SPV server - are community or private servers providing API access to light wallets clients.

They allow wallets running in the browser as well as desktop and mobile wallets that do not need to be online 24/7 nor reach consensus.

This project aims to provide implementation(s) of wallet servers for the Nyzo cryptocurrency.

## Goal of this project

Provide a simple to install and configure wallet server that users can run to provide an easy infrastructure for newcomers to use.  

- Simple endpoint for users (wallets) and services (shops)
- Eases onboarding
- stable and maintained wallet servers could end up rewarded by community funds

## Potential features

- json/rpc api
- websocket api
- get balance for a given address
- list (last?) transactions of an address
- send a client signed transaction to the cycle
- lookup a transaction by its txid

- auto install script
- Docker image

## Requirements

- Needs devs - backend, network, Docker
- Relies on [Open-db](../Open-DB/) + Nyzo client interaction for transaction sending. Close to a bitcoin like json-rpc implementation

## Contributors and how to help

See [Contributors](../contributors.md) for the list and introduction of the potential contributors.

Add an entry here with your handle and how you can help

### EggPool (EggdraSyl)
Can help with Design, specs, Python implementation, Docker.
