# Track

Track API is used to create, manage, and follow life cycle of **digital assets** on the blockchain. An asset is a digital representation of a real asset in the physical world. Through this API tracking the whole state changes of every asset can be implemented in an easy way, taking advantage of the inherit benefits from blockchain. 

## API Specification

An abstraction API with all the asset functionalities
### Asset
An asset is a digital representation of a real asset in the physical world. An asset records every single state or data change (f.e. the update of metadata, the transfer of ownership, etc.) This allow us to track the whole transactions since its creation in an inmutable and transparent way.

Every asset has the following structure:

- `assetid` :  `<string>` Unique identifier of the asset 
- `data`    :  `<json>`   JSON of **inmutable** data. It can have as many field as required
- `metadata`:  `<json>`   JSON of **mutable** data. It can have as many field as required
- `userOwner`:  `<string>` Owner of the asset
- `datetime` :  `<string>` UNIX date of creation
- `hftxid` :  `<string>` Current asset transaction in Hyperledger Fabric
- `trustpoint` : `<json>` JSON of data related to trustpoints. It can include the fields: EthereumContractAddres, LastEthTxId and LastHfTxId.
- `hash` :  `<string>` Hash of the asset


<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
    "assetid": "exampleAsset",
    "data": {
      "id":"A2839RP",
      "version":"1"
    },
    "metadata": {
      "color": "red"
      "position": { "x": "53", "y": "22"}
    },
    "userOwner": "test:telefonicaMSP"
    "datetime": 1558009289,
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "trustpoint": {
      "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
      "lastEthTxId":"0x6d9f4bb3fb67cc451758097c928777aa8adccb6c8a6e59c2c5bc9360208cc8b49"
    },
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
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
    "assetid": "",
    "data": {
      "id":"A2839RP",
      "version":"1"
    },
    "metadata" : {
      "color": "red",
      "position": { "x": 23.34, "y": -24.22}
    }
}
```
</details> 
<br>

*Output*
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "assetid": "exampleAsset",
    "data": {
      "id":"A2839RP",
      "version":"1"
    },
    "datetime": 1559820650,
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "trustpoint": {},
    "metadata": {
      "color": "red",
      "position": { "x": 23.34, "y": -24.22}
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
      "id":"A2839RP",
      "version":"1"
    },
    "datetime": 1559820650,
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "trustpoint": {},
    "metadata": {
      "color": "red",
      "position": { "x": 23.34, "y": -24.22}
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
        "id":"A2839RP",
        "version":"1"
      },
      "datetime": 1559820650,
      "hash": "zCZygxQBp5HBVm+SSUCCrgJfV3+CegaOzV9m+UxDsY8=",
      "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d06",
      "trustpoint": {},
      "metadata": {
        "color": "blue",
        "position": { "x": 98.35, "y": -12.32}
      },
      "userOwner": "test:org1MSP"
      },
    {
      "assetid": "exampleAsset",
      "data": {
        "id":"A2839RP",
        "version":"1"
      },
      "datetime": 1559820650,
      "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
      "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
      "trustpoint": {},
      "metadata": {
        "color": "red",
        "position": { "x": 23.34, "y": -24.22}
      }
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
<br>

*Output*
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "assetid": "exampleAsset",
    "data": {
      "id":"A2839RP",
      "version":"1"
    },
    "datetime": 1559820650,
    "hash": "oCZygxQBp5HBVm+SSUCCrgJfV3+CeghOzV9m+UxDsY8=",
    "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d05",
    "trustpoint":{},
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
    "color": "blue",
    "position": { "x": 98.35, "y": -12.32}
  }
}
```
</details> 
<br>

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
        "id":"A2839RP",
        "version":"1"
      },
      "datetime": 1559820650,
      "hash": "zCZygxQBp5HBVm+SSUCCrgJfV3+CegaOzV9m+UxDsY8=",
      "hftxid": "d249f267fd2dd58b6bff9d6780d31f3a04ab3a8c5b340b39ab48aed8fac55d06",
      "trustpoint": {},
      "metadata": {
        "color": "blue",
        "position": { "x": 98.35, "y": -12.32}
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
    "exampleAsset1",
    "exampleAsset2",
    "exampleAsset3"
  ]
}
```
</details>

---

#### (*) trustpoint parameter  
The `trustpoint` parameter is only filled in after the creation/registration of a trust point. Thus every new trust point regarding to an asset results in a new transaction in the asset with only the update of that parameter.

Transaction after creating a trustpoint in HF:

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
        "id":"A2839RP",
        "version":"1"
      },
      "datetime": 1559844444,
      "hash": "xfPsajse3rSSUCCrgJfV3+CegaOzV9m+ajso8sY=",
      "hftxid": "ac5f9d658b6bfaed8fd2dd40b39ab485d06780d31f3ad249f26704ab3a8c5b3f",
      "trustpoint": {
        "lastHfTxId":"dd40bdb76c439afd2bfaed6ad25b3ff5d0b80d315883a8984af3670bac549f2"
      },
      "userOwner": "test:org1MSP"
    }
  }
}
```
</details> 
<br>


Transaction after registering a trustpoint in Ethereum:

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
        "id":"A2839RP",
        "version":"1"
      },
      "datetime": 1559846666,
      "hash": "coAji3op2+SSUCCrgJfV3+CegaOzV9m+sodjPOI81=",
      "hftxid": "5aed880ddea2kf38d06b6bfd38ac2431f3aabab3adf9d6740b3fd2d9648fac55",
      "trustpoint": {
        "ethereumContractAddress": "0xeE83b6D6dc84fa0c91A6f99931f6CF29F6B7ea3b",
        "lastEthTxId":"0x6d9f4bb3fb67cc451758097c928777aa8adccb6c8a6e59c2c5bc9360208cc8b49"
      },
      "userOwner": "test:org1MSP"
    }
  }
}
```
</details> 

</details> 
<br>

## Architecture of the project
The project is based on the open-source programming language: Golang. An abstraction of its skeleton is depicted in the diagram below.

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

## How we run the application
As you could see in the [Architecture](architecture.html) module, all the applications are running on cloud. Through Kubernetes orchestration system the application deployment, scaling and management is an easy and automated task.

## Testing the Application
In postman folder there are the collection and environment to interact and test with the API methods. It is only needed to import them into postman application and know to use the coren-trackapi module

Also you can download the files in the links below:

<a href="_static/trackapi.collection.json" download> - Postman collection</a>
<br>
<a href="_static/environment.json" download> - Postman environment</a>

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

<br>