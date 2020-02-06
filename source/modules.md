# TrustOS

Why worrying about the low-level complexities of blockchain technology,
and having to worry about building you network when you can leverage
the benefits of the technology without having to know the details of
its operation. Our TrustOS abstracts all the complexity of blockchain
technology implementing the basic operations you need to leverage
the power of blockchain technology. 

**Table of Contents** 
- [Track API](#track-api)
- [Token API](#token-api)
- [Settlement API](#settlement-api)
- [ID API](#id-api)


## Login


In order to use the APIs, you need to have an active user and login to our system. Every API has a login method, which asks for a user and password.

A call to this method will return a JWT token, of this form:

```
{
  "message": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdCIsImV4cCI6MTU2MDAwMDE5MH0.M4PBSslERUImcOpWgg--N-2ZNW306BzWXTZVJgtdXWE"
}

```

Every call to the API, has to be authenticated, so the caller must provide this message as proof of his identity.

Add the following header to your HTTP request in order to authenticate your call: 

```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdCIsImV4cCI6MTU2MDAwMDE5MH0.M4PBSslERUImcOpWgg--N-2ZNW306BzWXTZVJgtdXWE
```


If you are calling the APIs from Postman, you can set manually the headers (there are examples in the miscelanea/postman folder)

However if you interact graphically with the swagger,  you have to click the button **authorize, on the top right** of the screen.


From there, in the "value" field of ApiKeyAuth, you should write:
```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdCIsImV4cCI6MTU2MDAwMDE5MH0.M4PBSslERUImcOpWgg--N-2ZNW306BzWXTZVJgtdXWE
```

You should now see that all the locks in swagger are closed, meaning that you are authenticated! 

The test user for this beta version is :
```
username : example
password : example
```

# TRACK API

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

# TOKEN API

This API allows developers to easily create transferable tokens on the Hyperledger Fabric network.

## API Specification

An abstraction API with all the token functionalities.

### Token

The term is a little bit confusing at first, since a token can represent the whole class, in which the total supply is declarated, or individual tokens (balances) transferable between users.

Every token has the following structure:
- `name` :  `<string>`  Name of the generic token
- `symbol` : `<string>` Shortname for the token
- `owner` :  `id<string>:company<string>`  Owner of the token. It has to be specified the ID of the owner and the ID of the organization it belongs to inside the organization
- `ethereumAddress`: `<string>` Address in the Ethereum blockchain, in case we want to link it to a public blockchain token
- `totalSupply` :  `<integer>` Total number of individual tokens issued
<details>

  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
      "name": "Test",
      "symbol": "Tst",
      "owner": "bteam:org1MSP",
      "ethereumAddress": "0x320492ua90suf9a0weuf903",
      "totalSupply": 99999999999999
}
```
</details>


<details>
  <summary><em><strong>Token methods</strong></em> (Click to expand)</summary>
---

#### POST   -   `/token/create/`

Creates a new generic token based on a chaincode

*Input*
- `name` :  `<string>`    Name of the token
- `symbol` : `<string>` Shortname of the token
- `owner` :  `identifier<string>:company<string>`   Owner of the token contract
- `ethereumAddress` :  `<string>` This address represents the contract in Ethereum associated to the token. At the moment is given as an input, but in future releases it will be created by the chaincode and given to the developer as a response 
- `totalSupply` :  `<integer>`  Total amount of individual tokens that will be created

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "name": "Test",
  "symbol": "Tst",
  "owner": "bteam:org1MSP",
  "ethereumAddress": "0x0",
  "totalSupply": 99999999999999
}

```
</details>

*Output*
- `message`    :  `<string>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "message": "Chaincode instantiated succesfully"
}

```
</details>



---

#### GET   -   `/token/{tokenId}`

Gets all the token info

*Input*
- `tokenId` :  `<string>`  Name of the token
  
*Output*
- `token`    :  `<string>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "output": {
    "name": "Test",
    "symbol": "Tst",
    "owner": "bteam:org1MSP",
    "ethereumAddress": "0x0",
    "totalSupply": 99999999999999
  }
}

```
</details>



---

#### GET   -   `/token/{tokenId}/allowance/{owner}/{spender}`

This call tells if some specific spender is allowed by some owner to performs actions over the token.

*Input*
- `tokenId` :  `<string>`  Name of the token
- `ownerId`   :  `<string>`  Owner of the token
- `spenderId` :  `<string>`  Person from whom we want to know how much he is allowed to spend
  
*Output*
- `allowed`  : `<integer>` Quantity of tokens he is allowed to spend

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "output": {
    "allowed": 230
  }
}
```
</details>


---

#### POST   -   `/token/{tokenId}/approve`
Approve a different spender for a amount of token you own

*Input*
- `tokenId` :  `<string>`  Name of the token
- `spender` :  `<string>` Name of the spender user
- `value`   :  `<int>`    Amount that is allowed to spend

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "spender": "Satoshi:org1MSP",
  "value": "20"
}

```
</details>
  
*Output*
- `id`    :  `<string>`  Id of the transaction
- `message`    :  `<string>`  Message of the approve transaction


<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "id": "eaff9d6d289ca1894cffb4bbx0e540de4f58f69eb067a23efba2b7581c77e398",
    "message": "Approve 230 from test:org1MSP to Satoshi:org1MSP"
  }
}

```
</details>



---

#### GET   -   `/token/{tokenId}/balance/{userID}`
Gets the token balance of a user

*Input*
- `tokenId` :  `<string>`  Name of the token
- `userId`  :  `<string>`  Name of the user
  
*Output*
- `balance`    :  `<integer>`  User's balance
- `blocked_balance`    :  `<integer>`  User's blocked balance

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "output": {
    "balance": 950,
    "blocked_balance": 50
  }
}

```
</details>


---

#### GET   -   `/token/{tokenId}/transactions`
Get the token transaction history

*Input*
- `tokenId` :  `<string>`  Id of the token
  
*Output*
- `list` :  `<json>`  List of transactions of the token

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "output": [
    {
      "id": "eaff9d6d289ca4894cffb4bbb0e540de4f58f69eb067a23efba2b7581c77e398",
      "message": "Approve 20 from test:org1MSP to Satoshi:org1MSP"
    },
    {
      "id": "5aa6239bb3c45647ab4ffa52759fc1fc981c28f8beb0724765b0c4505fca5a13",
      "message": "Transfer 40 from test:org1MSP to Bob:org1MSP"
    },
    {
      "id": "bb7f630b44a42b67abd437d4d9afb0b515fcd4b5794dd8cd6e3bf4f3510c5146",
      "message": "Transfer 40 from test:org1MSP to Alice:org1MSP"
    }
  ]
}

```
</details>



---

#### POST   -   `/token/{tokenId}/transfer`
Transfers individual tokens (balances of a token class)

*Input*
- `tokenId` :  `<string>`  Name of the token
- `to`      :  `<string>`  Destination user
- `value`   :  `<string>`  Balance to transfer

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "to": "Alice:org1MSP",
  "value": "40"
}

```
</details>
   
*Output*
- `id`    :  `<string>`  Id of the transaction
- `message`    :  `<string>`  Message of the approve transaction

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "id": "bb7f630b44a42b67abd437d4d9afb0b515fcd4b5794dd8cd6e3bf4f3510c5146",
    "message": "Transfer 40 from test:org1MSP to Alice:org1MSP"
  }
}

```
</details>


---

#### POST   -   `/token/{tokenId}/transferfrom`

Transfer / withdraw from a user. The user has to be approved to spend individual tokens

*Input*
- `from` :  `<string>`  Person who approves to spend. He has to have a positive balance
- `to`   :  `<string>`  Destination user of the funds
- `value`:  `<string>`  Amount of tokens

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "from": "bteam:org1MSP",
  "to": "satoshi:org1MSP",
  "value": "20"
}

```
</details>

*Output*
- `id`    :  `<string>`  Id of the transaction
- `message`    :  `<string>`  Message of the approve transaction

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "id": "7876322dbfe61fd2c293f63fd148875d36b3d4fbcec6635d55351bfab2e9e713",
    "message": "TransferFrom 20 from bteam:org1MSP to satoshi:org1MSP"
  }
}
```
</details>

---

#### POST   -   `/token/{tokenId}/transferownership`

Transfer the ownership of a generic token

*Input*
- `tokenId` :  `<string>`  Name of the token
- `to`      :  `<string>`  New owner

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "to": "Bob:org1MSP",
}

```
</details>

*Output*
- `token`  :  `<json>`  Token with updated parameters

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "output": {
    "ethereumAddress": "0x0",
    "name": "Test",
    "owner": "Bob:org1MSP",
    "symbol": "Tst",
    "totalSupply": 99999999999999
  }
}
```
</details>

---

#### POST   -   `/token/{tokenId}/transferblock`

Transfer individual tokens as a blocked balance for a user

*Input*
- `tokenId` :  `<string>`  Name of the token
- `to`      :  `<string>`  Destination user of the blocked funds
- `value`   :  `<string>`  Amount of tokens to be blocked

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
	"to":"bteam:org1MSP",
	"value":"50"
}

```
</details>

*Output*
- `blocked_id`    :  `<string>`  Id of the transaction
- `id`    :  `<string>`  Id of the transaction
- `message`    :  `<string>`  Message of the approve transaction

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "blocked_id": "7c76500379b86967c04490baa1d25ecc52adfc9df9340d561805b548d8c87e72",
    "id": "7c76500379b86967c04490baa1d25ecc52adfc9df9340d561805b548d8c87e72",
    "message": "Blocking transfer 50 from test:org1MSP to bteam:org1MSP"
  }
}
```
</details>


---

#### POST   -   `/token/{tokenId}/transferunblock`

Unblocks a blocked transfer being true equivalent to accept the blocked balance and false equivalent to returning the blocked balance to origin user

*Input*
- `tokenId`     :  `<string>`  Name of the token
- `blocked_id`  :  `<string>`  Id of the blocked transaction
- `accept`      :  `<string>`  Flag to determine the acceptance or not of the transaction

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "blocked_id": "b1cdd2e5df1d7565edb2c54ee39c0ab9931ea647d04627062cb52500ee82c0af",
  "accept": "true"
}

```
</details>

*Output*
- `id`    :  `<string>`  Id of the transaction
- `message`    :  `<string>`  Message of the approve transaction

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "output": {
    "id": "e309a55be8b1c842c3aaf475bb7b7b2b759101b09f622fbb5f8dc56aab3d3795",
    "message": "Accepting blocked transaction b1cdd2e5df0d7565bdb2c54ee39c0ab9931ea647d04627062cb52500ee82c0af from test:org1MSP and token amount goes to test:org1MSP"
  }
}
```
</details>

</details>

## Architecture of the project
```
coren-tokenapi
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
In postman folder there are the collection and environment to interact and test with the API methods. It is only needed to import them into postman application and know to use the coren-tokenapi module

## Errors management
  
  Token API errors are managed through the following nomenclature **TOKEN-XX** which corresponds to:<br>


  | Code 	| Description 	|
|:-----:	|-----------------------------------------------------------------------	|
| TOKEN-00 	| Service is down 	|
| TOKEN-01 	| Error parsing any data structure 	|
| TOKEN-02 	| Error of some kind of functionality 	|


# SETTLEMENT API

This API generates a general structure to perform the settlement of records. The API allows
the settlement of a great gamut of record structures, aggregations and settlement operations.
Currently two `aggregation` and `settlement` operations are implemented, but further
settlement and aggregation operations will be implemented in future versions. You can contact
our development team through the Issues to ask for new settlement and aggregation operations
to fit your use case.

## API Specification

An abstraction API with all the settlement functionalities.

### Settle

A settlement structure has the following parameters: 

- `settleid` :  `<string>`    - Unique identifier of the settlement structure
- `aggregates` : `<string >`  - Variables used as input for the aggregation operation.
- `primaryKey`    : `<string>` - Primary key used to aggregate metrics, build the common record and make the settlement.
- `aggregationType [1CDR / mcCounter]` : `<string >` - Aggregation operation. This operation is triggered every time a new record is updated to the system.
- `settlementType [1CDR / none]` : `<string>` - Settlement operation. It is triggered whenever a settlement operation is requested. It takes
the status of the common record and generates a settled structure. The aggregation variables are cleared for a new round of settlement.
- `record` : `<string>` - Sample record used to define the structure of records in the settlement structure. Also used as the
main variable used to upload records.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "settleid": "settle",
  "aggregates": "['msg']",
  "aggregationType": "mcCounter",
  "primaryKey": "app",
  "settlementType": "string",
  "record": {}
}

```
</details>



<details>
  <summary><em><strong>Settlement methods</strong></em> (Click to expand)</summary>

---
#### POST   -   `/settlement/create/`

Creates a new settlement structure. 

*Input*

- `settleid` :  `<string>`    - Unique identifier of the settlement structure
- `aggregates` : `<string >`  - Variables used as input for the aggregation operation.
- `primaryKey`    : `<string>` - Primary key used to aggregate metrics, build the common record and make the settlement.
- `aggregationType [1CDR / mcCounter]` : `<string >` - Aggregation operation. This operation is triggered every time a new record is updated to the system.
- `settlementType [1CDR / none]` : `<string>` - Settlement operation. It is triggered whenever a settlement operation is requested. It takes
the status of the common record and generates a settled structure. The aggregation variables are cleared for a new round of settlement.
- `record` : `<string>` - Sample record used to define the structure of records in the settlement structure. Also used as the
main variable used to upload records.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js

{
  "record": {
   "app":  "4240e1f7-d287-46a9-8b92-f112510bd9f7",
   "op":  "CREATE",
   "corr":  "AUS-b8727fc3-dfc1-4c37-b6d6-d6897ed10ddd"
  },
  "aggregates": ["op"],
  "aggregationType": "mcCounter",
  "settlementType": "none",
  "settleid": "testing",
  "primaryKey": "app"
 }
 ```
</details>
  
*Output*
- `settlementObject`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "aggregationMetrics": [
      "op"
    ],
    "aggregationType": "mcCounter",
    "lastSettlement": 1565172714,
    "lastUpdate": {
      "operation": "Create",
      "timestamp": 1565172714,
      "user": "test:org1MSP"
    },
    "primaryKey": "app",
    "settleid": "testing",
    "settlementType": "none"
  }
}


```
</details>


---

#### GET   -   `/settlement/{settleId}`

Gets the current status of a settlement structure. It shows the current
status of aggregates. 

*Input*
- `settleId` :  `<string>` 
  
*Output*
- `newSettlementObject`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "output": {
        "aggregates": {
            "2344240e1f7-d287-46a9-8b92-f1232342431": {
                "op": "2"
            },
            "4240e1f7-d287-46a9-8b92-f112510bd9f7": {
                "op": "1"
            }
        },
        "aggregationMetrics": [
            "op"
        ],
        "aggregationType": "mcCounter",
        "lastSettlement": 1565172714,
        "lastUpdate": {
            "operation": "Update",
            "timestamp": 1565172892,
            "user": "test:org1MSP"
        },
        "primaryKey": "app",
        "settleid": "testing",
        "settlementType": "none"
    }
}

```
</details>


---
#### GET   -   `/settlement/{settleId}/history`

Gets the history of changes over a settlement structure according to updated records.

*Input*
- `settleId` :  `<string>` 


  
*Output*
- `newSettlementObject`    :  `<json>` 


<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "output": [
        {
            "aggregates": {
                "2344240e1f7-d287-46a9-8b92-f1232342431": {
                    "op": "2"
                },
                "4240e1f7-d287-46a9-8b92-f112510bd9f7": {
                    "op": "1"
                }
            },
            "aggregationMetrics": [
                "op"
            ],
            "aggregationType": "mcCounter",
            "lastSettlement": 1565172714,
            "lastUpdate": {
                "operation": "Update",
                "timestamp": 1565172892,
                "user": "test:org1MSP"
            },
            "primaryKey": "app",
            "settleid": "testing",
            "settlementType": "none"
        },
        {
            "aggregationMetrics": [
                "op"
            ],
            "aggregationType": "mcCounter",
            "lastSettlement": 1565172714,
            "lastUpdate": {
                "operation": "Create",
                "timestamp": 1565172714,
                "user": "test:org1MSP"
            },
            "primaryKey": "app",
            "settleid": "testing",
            "settlementType": "none"
        }
    ]
}

```
</details>


---
#### GET   -   `/settlement/{settleId}/settled`

Gets all settlements performed over a specific settleId.

*Input*
- `settleId` :  `<string>` 


*Output*
- `newSettlementObject`    :  `<json>` 


<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "output": {
        "aggregates": {
            "2344240e1f7-d287-46a9-8b92-f1232342431": {
                "op": "2"
            },
            "4240e1f7-d287-46a9-8b92-f112510bd9f7": {
                "op": "1"
            }
        },
        "timestamp": 1565186196
    }
}

```
</details>



---
#### POST   -   `/settlement/{settleId}/update`

It uploads a new record to a settlement structure updating
the status of aggregates according to the `aggregationType` defined
for the settling structure. 

*Input*
- `settlementObject` :  `<json>`

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "record": [
    {
        "app":  "4240e1f7-d287-46a9-8b92-f112510bd9f7",
        "op":  "CREATE",
        "corr":  "AUS-b8727fc3-dfc1-4c37-b6d6-d6897ed10ddd"
        },
    {
        "app":  "2344240e1f7-d287-46a9-8b92-f1232342431",
        "op":  "CREATE",
        "corr":  "AUS-b8727fc3-dfc1-4c37-b6d6-d6897ed10ddd"
        },
    {
        "app":  "2344240e1f7-d287-46a9-8b92-f1232342431",
        "op":  "DELETE",
        "corr":  "AUS-b8727fc3-dfc1-4c37-b6d6-d6897ed10ddd"
        }
  ]
}


```
</details>
  
*Output*
- `newSettlementObject`    :  `<json>` 


<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "aggregates": {
      "2344240e1f7-d287-46a9-8b92-f1232342431": {
        "op": "2"
      },
      "4240e1f7-d287-46a9-8b92-f112510bd9f7": {
        "op": "1"
      }
    },
    "aggregationMetrics": [
      "op"
    ],
    "aggregationType": "mcCounter",
    "lastSettlement": 1565172714,
    "lastUpdate": {
      "operation": "Update",
      "timestamp": 1565172892,
      "user": "test:org1MSP"
    },
    "primaryKey": "app",
    "settleid": "testing",
    "settlementType": "none"
  }
}

```
</details>


---
#### POST  -   `/settlement/{settleId}/settle`

Settles a given settlement structure. It aggregates according to the
current status of aggregates and the `aggregationType` defined for the settlement
structure.

*Input*
- `settleId` :  `<string>` 
  
*Output*
- `newSettlementObject`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "output": {
        "2344240e1f7-d287-46a9-8b92-f1232342431": {
            "op": "2"
        },
        "4240e1f7-d287-46a9-8b92-f112510bd9f7": {
            "op": "1"
        }
    }
}

```
</details>



---
#### POST  -   `/settlement/{settleId}/clear`

Clears a settlement structure. It removes the current status of the aggregates.
This may be used when unconsistent updates have been performed or errors have
been detected in the updating of records.

*Input*
- `settleId` :  `<string>` 
  
*Output*
- `newSettlementObject`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "output": {
        "aggregationMetrics": [
            "op"
        ],
        "aggregationType": "mcCounter",
        "lastSettlement": 1565186196,
        "lastUpdate": {
            "operation": "Clear",
            "timestamp": 1565186640,
            "user": "test:org1MSP"
        },
        "primaryKey": "app",
        "settleid": "testing",
        "settlementType": "none"
    }
}
```
</details>
</details>

## Architecture of the project
```
coren-tokenapi
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
├── vendor                  // Package discovery folder
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
In postman folder there are the collection and environment to interact and test with the API methods. It is only needed to import them into postman application and know to use the coren-settleapi module

## Errors management
  
  Settle API errors are managed through the following nomenclature **SETTLE-XX** which corresponds to:<br>


  | Code 	| Description 	|
|:-----:	|-----------------------------------------------------------------------	|
| SETTLE-00 	| Service is down 	|
| SETTLE-01 	| Error parsing any data structure 	|
| SETTLE-02 	| Error of some kind of functionality 	|





## ID API
This API manages all about identity in the TRUST OS.

**NOTE: This is a work in progress, more about this in future releases.**