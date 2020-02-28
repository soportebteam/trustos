# Track

This API is used to create, manage, and export digital assets on the blockchain.

## API Specification

An abstraction API with all the asset functionalities
### Asset
An asset is a digital representation of a real asset in the real world. 

Every asset has the following structure:

- `assetid` :  `<string>` Unique identifier of the asset 
- `data`    :  `<json>`   JSON of **inmutable** data.
- `metadata`:  `<json>`   JSON of **mutable** data.
- `userOwner`:  `<string>` Owner of the asset
- `datetime` :  `<string>` Timestamp of creation
- `hftxid` :  `<string>` Current asset transaction in Hyperledger Fabric
- `ethereumContractAddress` :  `<string>` The smart contract in Ethereum to manage trust points
- `lastEthTxId` :  `<string>` Last asset transaction in Ethereum
- `hash` :  `<string>` Hash of the asset


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
    "metadata": {
      "color": "red"
    },
    "userOwner": "test:org1MSP",
    "datetime": 1558009289,
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
    "lastEthTxId": "0x6d9f4bb3fb67cc451758097c928777aa8adccb6c8a6e59c2c5bc9360208cc8b49",
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8="
}

```
</details> 
<br>

### Methods

![TrackAPI methods](./images/track_swagger.png)

<details>
  <summary><em><strong> Asset methods</strong></em> (Click to expand)</summary>

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
<br>

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


<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-0pky">Code</th>
    <th class="tg-0pky">Description</th>
  </tr>
  <tr>
    <td class="tg-0pky">TRACK-00</td>
    <td class="tg-0pky">Service is down</td>
  </tr>
  <tr>
    <td class="tg-0pky">TRACK-01</td>
    <td class="tg-0pky">Error parsing any data structure</td>
  </tr>
  <tr>
    <td class="tg-0lax">TRACK-02</td>
    <td class="tg-0lax">Error of some kind of functionality</td>
  </tr>
</table>

