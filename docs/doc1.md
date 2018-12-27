---
id: doc1
title: Getting Started
sidebar_label: Example Page
---

<!-- Check the [documentation](https://docusaurus.io) for how to use Docusaurus. -->

## Clone the repo and install the project

1. git clone  https://github.com/ledgerium/governanceApp.git
2. cd governanceApp

## Bring up the geth nodes using docker compose

NOTE: If there are existing docker instances (sudo docker ps -a), stop and remove them

```
sudo docker stop $(sudo docker ps -aq)
```
```
sudo docker rm $(sudo docker ps -aq)
```

1. Create docker network by running this command
    ```
    docker network create -d bridge --subnet 172.16.239.0/24 --gateway 172.16.239.1 app_net
    docker network create -d bridge --subnet 172.19.240.0/24 --gateway 172.19.240.1 test_net
    ```
2. Run the geth nodes by running docker-compose up -d

## We are not using truffle framework for any compilation

sudo npm install -g truffle

truffle compile

```
We have used solc compiler to AdminValidatorSet and SimpleValidatorSet contract
- solc --overwrite --gas --bin-runtime --abi --optimize-runs=200 -o ./build/contracts ./contracts/AdminValidatorSet.sol
- solc --overwrite --gas --bin-runtime --abi --optimize-runs=200 -o ./build/contracts ./contracts/SimpleValidatorSet.sol
- npm install
```

## Run the smart contracts - Usages

The governanceApp can be used with different switches

protocol

    1. ws
    2. http

hostname

    1. localhost
    2. XXX.XXX.XXX.XXX

port

    1. e.g. 9000 for Websocket
    2. 8545 for http

readkeyconfig

    if keystore\privatekey.json needs to be used for accounts and respective their private keys

or privateKeys

    provide comma-seperated valid private keys like "897c0cee04cadac8df147671bc0868c208c95c750d46be09f2d7b18b4efabdbb"

runadminvalidator - for AdminValidatorSet tests

    1. runAdminTestCases
    2. runRemoveAdminTestCases
    3. getAllActiveAdmins
    4. getAllAdmins
    5. addOneAdmin
    6. removeOneAdmin
    7. runClearProposalsAdminTestCases -- provide valid ethereum address with comma 
       e.g.0xc2cb28fad9b82036c9f32cbd6c84343612ee0323

runsimplevalidator - for SimpleValidatorSet tests

    1. validatorSetup
    2. runValidatorTestCases
    3. runRemoveValidatorTestCases
    4. getListOfActiveValidators
    5. addSimpleSetContractValidatorForAdmin -- provide valid ethereum address with comma 
       e.g. "0xc2cb28fad9b82036c9f32cbd6c84343612ee0323"
    6. removeSimpleSetContractValidatorForAdmin -- provide valid ethereum address with comma 
       e.g. "0xc2cb28fad9b82036c9f32cbd6c84343612ee0323"

## Sample usages

```
node index.js protocol=ws hostname=localhost port=9000 privateKeys=7e0d243242af3a907f7b0675925bf1694d1e586265b4fc9dc4f20e2a1157f4e3
```

Running with events ON - with the ws switch

```
node index.js protocol=ws hostname=localhost port=9000 readkeyconfig=true runsimplevalidator=getListOfActiveValidators,addSimpleSetContractValidatorForAdmin,0xf1cba7514dcf9d1e8b1151bcfa05db467c0dcf1a,removeSimpleSetContractValidatorForAdmin,0xf1cba7514dcf9d1e8b1151bcfa05db467c0dcf1a
```

Running 'without' events ON - with the http switch

```
node index.js protocol=http hostname=localhost port=8545 readkeyconfig=true runadminvalidator=addOneAdmin,0x3a91fd8517b58470c85fd570913b358c4db916bc,runClearProposalsAdminTestCases,0xc2cb28fad9b82036c9f32cbd6c84343612ee0323,getAllActiveAdmins
```

## Running the smart contracts testcases

'npm test' This will run testcases of the AdminValidatorSet and SimpleValidatorSet contracts on local setup

This will bring up

    1. 7 geth node docker instances
    2. 7 corresponding constellation node docker instances
    3. 1 quorum-maker front end app docker instance
    4. 1 eth-stat front end app docker instance


