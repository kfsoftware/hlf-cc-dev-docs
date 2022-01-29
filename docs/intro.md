---
sidebar_position: 1
---

# Intro

Let's discover **Docusaurus in less than 5 minutes**.

## Getting Started

`hlf-cc-dev` is a tool to start developing a new chaincode from your development environment.

### What you'll need

- A TLS/TCP tunnel to your local development environment (ngrok, getout, etc.)
- Hyperledger Fabric peer with external chaincode builder enabled.
- Network config with admin users for all of the organizations peers you will use.

## General diagram

The following diagram explains the architecture of the final solution

![Diagram](/img/diagram.png)


## Steps to get started

To start the server you need the network config with the admin users for each orga

```bash
hlf-cc-dev serve --address ":8080" --metrics-address ":8081" --config "<PATH_TO_NETWORK_CONFIG>"
```

## Start development on your local environment

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


