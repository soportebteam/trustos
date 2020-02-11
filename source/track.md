# Track

This API is used to create, manage, and export digital assets on the blockchain.

## API Specification

An abstraction API with all the asset functionalities
### Asset
An asset is a digital representation of a real asset in the real world. 

Every asset has the following structure:

- `assetid` :  `<string>` Unique identifier of the asset 
- `data`    :  `<json>`   JSON of **inmutable** data. It can have as many field as required
- `datetime` :  `<string>` UNIX date of creation
- `ethereumContractAddress` :  `<string>` The smart contract in Ethereum to manage trust points
- `hash` :  `<string>` Hash of the asset
- `hftxid` :  `<string>` Last asset transaction in Hyperledger Fabric
- `lastEthTxId` :  `<string>` Last asset transaction in Ethereum
- `metadata`:  `<json>`   JSON of **mutable** data. It can have as many field as required
- `userOwner`:  `<string>` Owner of the asset

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "assetid": "exampleAsset",
    "data": {
      "position": {
        "x": "53",
        "y": "22"
      }
    },
    "datetime": 1558009289,
    "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "lastEthTxId": "0x6d9f4bb3fb67cc451758097c928777aa8adccb6c8a6e59c2c5bc9360208cc8b49",
    "metadata": {
      "color": "red"
    },
    "userOwner": "test:org1MSP"
}

```
</details> 

<details>
  <summary><em><strong>Asset methods</strong></em> (Click to expand)</summary>

---

####     POST -  `/asset/create` 
Ceate a digital asset on a Blockchain. 

*Input*
- `assetid` :  `<string>` Unique identifier of the asset
- `data`    :  `<json>` JSON of **inmutable** data. It can have as many field as required
- `metadata`:  `<json>` JSON of **mutable** data. It can have as many field as required

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "assetid": "exampleAsset2",
    "data": {
      "color": "red"
    },
    "metadata" : {
      "position":{
        "x": 23.34,
        "y": -24.22
      }
    }
    }
}
```
</details> 

*Output*
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "assetid": "exampleAsset",
    "data": {
      "color": "red"
    },
    "datetime": 1559820650,
    "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "lastEthTxId": "",
    "metadata": {
      "position": {
        "x": 23.34,
        "y": -24.22
      }
    }
    "userOwner": "test:org1MSP"
  }
}
```
</details> 

---

####    GET     -   `/asset/{assetId}`  


Get asset from the blockchain identified by assetId

*Input*
- `assetid` :  `<string>` Unique identifier of the asset
  
*Output*
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "assetid": "exampleAsset",
    "data": {
      "color": "red"
    },
    "datetime": 1559820650,
    "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "lastEthTxId": "",
    "metadata": {
      "position": {
        "x": 23.34,
        "y": -24.22
      }
    }
    "userOwner": "test:org1MSP"
  }
}
```
</details> 

---

####   GET  -     `/asset/{assetId}/transactions`  

Get all transactions for the whole lifecycle of the asset

*Input*
- `assetid` :  `<string>` Unique identifier of the asset

*Output*
- `args`    :  `<string>` A list of all transactions

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": [
    {
      "assetid": "exampleAsset",
      "data": {
        "color": "red"
      },
      "datetime": 1559820650,
      "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
      "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
      "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
      "lastEthTxId": "",
      "metadata": {
        "position": {
          "x": 23.34,
          "y": -24.22
        }
      }
      "userOwner": "test:org1MSP"
      },
    {
      "assetid": "exampleAsset",
      "data": {
        "color": "red"
      },
      "datetime": 1559820650,
      "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
      "hash": "zCZygxQBp5HBVm+SSUCCrgJfV3+CegaOzV9m+UxDsY8=",
      "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d06",
      "lastEthTxId": "",
      "metadata": {
        "position": {
          "x": 98.35,
          "y": -12.32
        }
      },
      "userOwner": "test:org1MSP"
    }
  ]
}

```
</details>

---

####   POST     - `/asset/{assetId}/transfer`  

Transfer the ownership of the asset. The user has to be the owner of the asset.

*Input*
- `assetid` :  `<string>` Unique identifier of the asset
- `destinationId` :  `<string>` The destination owner

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "destinationId": "bteam",
}
```
</details> 

*Output*
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "assetid": "exampleAsset",
    "data": {
      "color": "red"
    },
    "datetime": 1559820650,
    "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "lastEthTxId": "",
    "metadata": {
      "position": {
        "x": 23.34,
        "y": -24.22
      }
    }
    "userOwner": "bteam"
  }
}
```
</details>

---

####  POST    `/asset/{assetId}/update`  

Updates the **mutable** ("metadata") of an asset
*Input*
- `assetid` :  `<string>` Unique identifier of the asset
- `metadata`:  `<json>` JSON of **mutable** data. It can have as many field as required

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "metadata": {
    "position": {
      "x": 98.35,
      "y": -12.32
    }
  }
}
```
</details> 

*Output*
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    {
      "assetid": "exampleAsset",
      "data": {
        "color": "red"
      },
      "datetime": 1559820650,
      "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
      "hash": "zCZygxQBp5HBVm+SSUCCrgJfV3+CegaOzV9m+UxDsY8=",
      "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d06",
      "lastEthTxId": "",
      "metadata": {
        "position": {
          "x": 98.35,
          "y": -12.32
        }
      },
      "userOwner": "test:org1MSP"
    }
  }
}
```
</details> 

---

#### GET   -    `/assets`  

Lists all the assets of a user

*Input*
 N/A. It returns all the assets which belong to the login user

*Output*
- `assetList`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": [
    "exampleAsset",
    "exampleAsset110",
    "exampleAsset133"
  ]
}
```
</details>

</details> 

### Trust

Trustpoints are `<JSON>` objects used to export the integrity of the transactions over an asset in a private blockchain such as Hyperledger Fabric, to public blockchains such as Ethereum, in order to provide an extra layer of security.


This is the structure of a trust point:

- `assetid` :  `<string>` Identifier of the asset for which the trust point is made
- `end` :  `<integer>` Timestamp at which this trust point is made
- `ethereumContractAddress` :  `<string>` The smart contract in Ethereum to manage trust points
- `hash` :  `<string>`  Hash of the trust point (as a JSON) to verify integrity
- `txRoot` :  `<string>` Hash of all transactions in the interval
- `hftxid` :  `<string>` Last trust transaction in Hyperledger Fabric
- `init` :  `<integer>` Timestamp for the previous trust point
- `prevHash` :  `<string>` Hash of the previous trust point
- `prevhftxid` :  `<string>`  Hash of the previous transaction (in the blockchain)

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "assetid": "exampleAsset",
    "end": 1557830077,
    "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99971f6CF29F6B7ea3b",
    "hash": "3P1HZ+pvbwhogR3tgKng7cWTk6uaHynGKvjqPjpISi0=",
    "txRoot": "DGjUiCplVGom99o6bbdIXAIEqNKgVoQGi7rFNwDX+to=",
    "hftxid": "671e8c065add74a4759167b9f38cf67916f0f26b5e9b1861c2abcb08a57f8a97",
    "init": 0,
    "prevHash": "",
    "prevhftxid": "0"
  }
}

```
</details>
<details>
  <summary><em><strong>Trust methods</strong></em> (Click to expand)</summary>

---

#### GET  -   `/trust/assetId`  

Gets the last trust point in the system for a specific asset

*Input*
- `assetid` :  `<string>` Identifier of the asset for which the trust point is made
  
*Output*
- `trustpoint`    :  `<json>`

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
      "assetId": "exampleAsset",
      "end": 1567601354,
      "ethereumContractAddress": "0x1B646bc6C3465Fa8171F7171097A7d8e37b43D6B",
      "hash": "7KYLJXcjGA67WD0v95UvoVPk+sj9M8FdpecS5mRz3+s=",
      "hfTxId": "5c709f206555dbc6a40e37e96aa007a471f706927c8581fb91aef3625413e234",
      "init": 1567594895,
      "prevHash": "Ni7JYQG6GSmlEjWoRj2xrfF6ZVFhqBDPzyjk+o/HB2c=",
      "prevHfTxId": "70c26cfc9aeef3c094b82278b7ed413255f07711366ac2a9da8de7e66b9e53ee",
      "txRoot": "TBSNvFDt3tGDhI5I48IRlBh2l+O0X+kjBq7/96Zk/wI="
    }
}

```
</details>

---

#### GET  -   `/trust/assetId/history`  

Gets all trust point history in the system for a specific asset

*Input*
- `assetid` :  `<string>` Identifier of the asset for which the trust point is made
  
*Output*
- `trustpoint`    :  `<json>`

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
[{
  "output": [
    {
      "assetId": "exampleAsset",
      "end": 1567594895,
      "ethereumContractAddress": "0x1B646bc6C3465Fa8171F7171097A7d8e37b43D6B",
      "hash": "Ni7JYQG6GSmlEjWoRj2xrfF6ZVFhqBDPzyjk+o/HB2c=",
      "hfTxId": "70c26cfc9aeef3c094b82278b7ed413255f07711366ac2a9da8de7e66b9e53ee",
      "init": 0,
      "prevHfTxId": "0",
      "txRoot": "oGFYgnxCcPvpa2d6G4vHLs92HQgY2z6S8uwIVM0Qg44="
    },
    {
      "assetId": "exampleAsset",
      "end": 1567601354,
      "ethereumContractAddress": "0x1B646bc6C3465Fa8171F7171097A7d8e37b43D6B",
      "hash": "7KYLJXcjGA67WD0v95UvoVPk+sj9M8FdpecS5mRz3+s=",
      "hfTxId": "5c709f206555dbc6a40e37e96aa007a471f706927c8581fb91aef3625413e234",
      "init": 1567594895,
      "prevHash": "Ni7JYQG6GSmlEjWoRj2xrfF6ZVFhqBDPzyjk+o/HB2c=",
      "prevHfTxId": "70c26cfc9aeef3c094b82278b7ed413255f07711366ac2a9da8de7e66b9e53ee",
      "txRoot": "TBSNvFDt3tGDhI5I48IRlBh2l+O0X+kjBq7/96Zk/wI="
    }
  ]
]

```
</details>

---



#### POST -  `/trust/assetId/create`  

Creates a trust point in the system for a specific asset

*Input*
- `assetid` :  `<string>` Identifier of the asset for which the trust point is made
  
*Output*
- `trustpoint`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
      "assetId": "exampleAsset",
      "end": 1567601354,
      "ethereumContractAddress": "0x1B646bc6C3465Fa8171F7171097A7d8e37b43D6B",
      "hash": "7KYLJXcjGA67WD0v95UvoVPk+sj9M8FdpecS5mRz3+s=",
      "hfTxId": "5c709f206555dbc6a40e37e96aa007a471f706927c8581fb91aef3625413e234",
      "init": 1567594895,
      "prevHash": "Ni7JYQG6GSmlEjWoRj2xrfF6ZVFhqBDPzyjk+o/HB2c=",
      "prevHfTxId": "70c26cfc9aeef3c094b82278b7ed413255f07711366ac2a9da8de7e66b9e53ee",
      "txRoot": "TBSNvFDt3tGDhI5I48IRlBh2l+O0X+kjBq7/96Zk/wI="
    }
}

```
</details>

---

#### GET  -   `/trust/{assetId}/merkleroot`  

Gets the last trust merkle root stored in the system

*Input*
- `assetid` :  `<string>` Identifier of the asset for which the trust root is stored
  
*Output*
- `trustroot`    :  `<json>`

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "timestamp": 1567601354,
    "trustHash": "7KYLJXcjGA67WD0v95UvoVPk+sj9M8FdpecS5mRz3+s=",
    "trustRoot": "/unY4B8YDNq/+mdO1iL/Ztng+gbxBput2qnjG+LGMqU="
  }
}

```
</details>

---

#### GET  -   `/trust/{assetId}/merkleroot/history`  

Gets the trust merkle root history stored in the system

*Input*
- `assetid` :  `<string>` Identifier of the asset for which the trust root is stored
  
*Output*
- `trustroot`    :  `<json>`

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": [
    {
      "timestamp": 1567594895,
      "trustHash": "Ni7JYQG6GSmlEjWoRj2xrfF6ZVFhqBDPzyjk+o/HB2c=",
      "trustRoot": "Vz3ZFr+wTOt0FNbcfhEr+Ziy/Y/jsfNGz693KcqYa5E="
    },
    {
      "timestamp": 1567601354,
      "trustHash": "7KYLJXcjGA67WD0v95UvoVPk+sj9M8FdpecS5mRz3+s=",
      "trustRoot": "/unY4B8YDNq/+mdO1iL/Ztng+gbxBput2qnjG+LGMqU="
    }
  ]
}

```
</details>

---

#### POST -  `/trust/assetId/register`  

Creates a trust point if does not exist and registers it in Ethereum. If the trust point already exists registers it in Ethereum.

*Input*
- `assetid` :  `<string>` Identifier of the asset for which the trust point is made
  
*Output*
- `trustpoint` :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output":  {
      "assetId": "exampleAsset",
      "end": 1567601354,
      "ethereumContractAddress": "0x1B646bc6C3465Fa8171F7171097A7d8e37b43D6B",
      "hash": "7KYLJXcjGA67WD0v95UvoVPk+sj9M8FdpecS5mRz3+s=",
      "hfTxId": "5c709f206555dbc6a40e37e96aa007a471f706927c8581fb91aef3625413e234",
      "init": 1567594895,
      "prevHash": "Ni7JYQG6GSmlEjWoRj2xrfF6ZVFhqBDPzyjk+o/HB2c=",
      "prevHfTxId": "70c26cfc9aeef3c094b82278b7ed413255f07711366ac2a9da8de7e66b9e53ee",
      "txRoot": "TBSNvFDt3tGDhI5I48IRlBh2l+O0X+kjBq7/96Zk/wI="
    }
}

```
</details>

---

#### POST   -   `/trust/assetId/verify`

Verifies a trust point 

*Input*
- `assetid` :  `<string>` Identifier of the asset for which the trust point is made
- `timestamp` : `<string>` Timestamp at which this trust point is made

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "timestamp": "1559822594",
}

```
</details>

*Output*
- `ethereum`:  `<json>` Ethereum info
  - `trustRoot`:  `<string>` Trust points merkle root registered on Ethereum
  - `lastEthTxId`:  `<string>` Last transaction for the trust point in Ethereum
  - `smartContractAddres`:  `<string>` The smart contract in Ethereum to manage trust points 
  - `verified`:  `<bool>` Boolean value to specify if the trust point is registered in Ethereum
- `hf`:  `<json>` Hyperledger Fabric info
  - `trustRoot`:  `<string>` Trust points merkle root stored in HF
  - `timestamp`:  `<string>` Timestamp at which this trust point is made
  - `verified`:  `<bool>` Boolean value to specify if the trust point is registered in Ethereum and it is has not been modified


<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "output": {
    "ethereum": {
      "lastEthTxId": "0x8ad8f928c261a5b7f2b6515320dfffe1f9f923b17c5e07f6f733f43703f95f87",
      "smartContractAddres": "0x1B646bc6C3465Fa8171F7171097A7d8e37b43D6B",
      "trustHash": "NGz693K+cqYasFNbcfhEr+Ziy/Y/jsfOt0FNKcqYa5E=",
      "trustRoot": "/unY4B8YDNq/+mdO1iL/Ztng+gbxBput2qnjG+LGMqU=",
      "verified": true
    },
    "hf": {
      "timestamp": 1567601354,
      "trustHash": "NGz693K+cqYasFNbcfhEr+Ziy/Y/jsfOt0FNKcqYa5E=",
      "trustRoot": "/unY4B8YDNq/+mdO1iL/Ztng+gbxBput2qnjG+LGMqU=",
      "verified": true
    }
  }
}

```
</details>
</details>

### MerkleRoot

In order to achieve the integrity and inmutability of all trust points, every time a trust point is create a parallel process is executed. This process consist of the building of a trust-based merkle tree. All the trust points created until that moment are the leaves of the tree that generates a unique merkle root. That merkle root, called as trustRoot, is registered in HF as well as in Ethereum to proof the integrity. So, every time a new trust point is created, a new trustRoot is created too, and it could be registered in Ethereum or not, depends of the user neccessity


This is the structure registered in HF and Ethereum, once the trust merkle tree is calculated:

- `timestamp` :  `<integer>` Timestamp at which the related trust point is made
- `trustHash` :  `<string>` Hash of the last trust point included to verify integrity
- `trustRoot` :  `<string>` Root of the trust merkle tree calculated with all the trust points until that moment

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "timestamp": 1567601354,
    "trustHash": "7KYLJXcjGA67WD0v95UvoVPk+sj9M8FdpecS5mRz3+s=",
    "trustRoot": "/unY4B8YDNq/+mdO1iL/Ztng+gbxBput2qnjG+LGMqU="
  }
}

```
</details>

## Architecture of the project
```
coren-trackapi
├── api
      ├── handler           // HTTP logic
      ├── model             // models used by the application
      ├── service           // Usecases logic
      ├── util              // Tools used by the application
          ├── log           // Logger tool
          ├── http          // Http util
          └── Config        // Tool to load the configuration from yaml files
      └── app.go            // Router application
├── config
      └── config.yaml       // Config file
├── docs
      └── docs.go           // Swagger doc file
├── postman                 // Postman collection and environment to test the API
      ├── collection    
      └── environment
├── docker-compose.yaml     // Instructions to build docker container
├── Dockerfile              // Instructions to build docker image
├── init.sh                 // Script with global environment variables
└── main.go                 // Main app
 ```   

## Project configuration
This project has too bee stored in the following route:
```
$GOPATH/src/github.com/name_of_the_project
```

## Running the Application
To initialize the application execute the following commands:
```
source ./init.sh
go run main.go
```

Also the application can be executed with docker:
```
docker-compose up -d
```

## Testing the Application
In postman folder there are the collection and environment to interact and test with the API methods. It is only needed to import them into postman application and know to use the coren-trackapi module

## Errors management
  
  Track API errors are managed through the following nomenclature **TRACK-XX** which corresponds to:<br>


  | Code 	| Description 	|
|:-----:	|-----------------------------------------------------------------------	|
| TRACK-00 	| Service is down 	|
| TRACK-01 	| Error parsing any data structure 	|
| TRACK-02 	| Error of some kind of functionality 	|

