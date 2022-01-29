---
sidebar_position: 1
---

# Intro

## What's `hlf-cc-dev`?

`hlf-cc-dev` is a tool to start developing a new chaincode from your development environment.

### Why does this tool exist?

When developing chaincodes, we need to have an HLF network deployed, usually in our development environment, which is hard for new developers to get started since they need to know how to deploy an HLF network.

This tool aims to ease the onboarding of new developers that are not familiar with the internals of the HLF network but are interested in developing chaincodes.

The only requirement is that the developer has access to a working HLF network, this network can be set up by Administrators that are used to perform these operations, so the developer doesn't need to.

With this tool, instead of installing the chaincode in the peers, approving the chaincode definition, and finally, committing the chaincode, the developer can have the chaincode started in its machine, and with one command, it can install, approve and commit the chaincode in one go. If the developer needs to modify the chaincode logic, all it needs to do is restart the chaincode program running in its machine, just like any other application the developer is used to developing.

### What you'll need

- A TLS/TCP tunnel to your local development environment (ngrok, getout, etc.)
- Hyperledger Fabric peer with external chaincode builder enabled.
- Network config with admin users for all of the organizations peers you will use.

## General diagram

The following diagram explains the architecture of the final solution

![Diagram](/img/diagram.png)


## Steps to get started

To start the server, you need the network config with the admin users for each organization.

```bash
hlf-cc-dev serve --address ":8080" --metrics-address ":8081" --config "<PATH_TO_NETWORK_CONFIG>"
```

## Start development in your local environment

```bash
CHAINCODE_NAME=chaincode1
API_URL="http://localhost:8080/graphql"
SIGNATURE_POLICY="OR('Org1MSP.member', 'Org2MSP.member')"
CHAINCODE_ADDRESS_TUNNEL="4.tcp.eu.ngrok.io:13438" # can be found in ngrok output
hlf-cc-dev start --localChaincode="localhost:9999" \
  --chaincodeAddress="${CHAINCODE_ADDRESS_TUNNEL}" \
  --signaturePolicy="${SIGNATURE_POLICY}" \
  --chaincode="${CHAINCODE_NAME}" \
  --apiUrl="${API_URL}" \
  --env-file="${PWD}/.env" \
  --pdc=./pdc.json
```


