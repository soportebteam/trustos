# Track

Track API is used to create, manage, and follow life cycle of **digital assets** on the blockchain. An asset is a digital representation of a real asset in the physical world. Through this API tracking the whole state changes of every asset can be implemented in an easy way, taking advantage of the inherit benefits from blockchain. 

## API Specification

An abstraction API with all the asset functionalities.
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

### Authorised assets

There are two types of assets: owned assets and authorised assets. These last ones, the `authorised assets`  are assets created by other users that have granted you access allowing you to consult and update it. 

In order to interact with both assets in some functions it is necessary to set a flag formely known as `isAuthorised`. In order to interact with authorised, only it is necessary to put the `isAuthorised` flag to `true` as a query parameter in the URL (`...?isAuthorised=true`) as it is shown in the examples below:

- GET  -     `/asset/{assetId}?isAuthorised=true`  
- GET  -     `/asset/{assetId}/transactions?isAuthorised=true`  
- POST  -     `/asset/{assetId}/transactions/range?isAuthorised=true`  
- GET  -     `/assets?isAuthorised=true`  
- POST -     `/asset/{assetId}/update?isAuthorised=true`  

## API Methods

![TrackAPI methods](./images/track_swagger.png)

<details>
  <summary><em><strong> Asset methods</strong></em> (Click to expand)</summary>

---

####     POST -  `/asset/create` 
Ceate a digital asset on a Blockchain. 

<u>*Input*</u>
- `assetid` :  `<string>` Unique identifier of the asset.
- `data`    :  `<json>` JSON of **inmutable** data. It can have as many field as required.
- `metadata`:  `<json>` JSON of **mutable** data. It can have as many field as required.

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

<u>*Output*</u>
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

####    GET     -   `/asset/{assetId}?isAuthorised=boolean`  


Get asset from the blockchain identified by assetId.

<u>*Input*</u>
- `assetid` :  `<string>` Unique identifier of the asset.
- `isAuthorised`: `<boolean>` Flag to get own (false) or authorised (true) assets.

(*) Please navigate to the following [section](#authorised-assets) for isAuthorised query param details.
  
<u>*Output*</u>
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

####   GET  -     `/asset/{assetId}/transactions?isAuthorised=boolean`  

Get all transactions for the whole lifecycle of the asset.

<u>*Input*</u>
- `assetid` :  `<string>` Unique identifier of the asset.
- `isAuthorised`: `<boolean>` Flag to get own (false) or authorised (true) assets.

(*) Please navigate to the following [section](#authorised-assets) for isAuthorised query param details.

<u>*Output*</u>
- `args`    :  `<string>` A list of all transactions.

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

####   POST  -     `/asset/{assetId}/transactions/range?isAuthorised=boolean`  

Get all transactions within a range for the whole lifecycle of the asset.

<u>*Input*</u>
- `assetid` :  `<string>` Unique identifier of the asset.
- `isAuthorised`: `<boolean>` Flag to get own (false) or authorised (true) assets.
- `rangeAsset`    :  `<json>` JSON object to define range.

(*) Please navigate to the following [section](#authorised-assets) for isAuthorised query param details.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "init": "0",
  "end": "1575975331"
}
```
</details>
<br>


<u>*Output*</u>
- `args`    :  `<string>` A list of all transactions.

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

<u>*Input*</u>
- `assetid` :  `<string>` Unique identifier of the asset.
- `destinationId` :  `<string>` The destination owner.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "destinationId": "bteam",
}
```
</details> 
<br>

<u>*Output*</u>
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

####  POST    `/asset/{assetId}/update?isAuthorised=boolean`  

Updates the **mutable** ("metadata") of an asset.

<u>*Input*</u>

- `assetid` :  `<string>` Unique identifier of the asset.
- `isAuthorised`: `<boolean>` Flag to update own (false) or authorised (true) assets.
- `metadata`:  `<json>` JSON of **mutable** data. It can have as many field as required.

(*) Please navigate to the following [section](#authorised-assets) for isAuthorised query param details.

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

<u>*Output*</u>
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


####   POST     - `/asset/{assetId}/authorise`  

Authorise user access for an asset. Only the asset owner can do this.

<u>*Input*</u>
- `assetId` :  `<string>` Unique identifier of the asset.
- `userId` :  `<string>` The authorised user.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "userId": "did:bteam"
}
```
</details> 
<br>

<u>*Output*</u>
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "message": "Successfully authorised user did:bteam for asset XXXXX",
  }
}
```
</details>

---

####   POST     - `/asset/{assetId}/unauthorise`  

Unauthorise user access for an asset. Only the asset owner can do this.

<u>*Input*</u>
- `assetId` :  `<string>` Unique identifier of the asset.
- `userId` :  `<string>` The unauthorised user.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "userId": "did:bteam"
}
```
</details>  
<br>

<u>*Output*</u>
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "message": "Successfully unauthorised user did:bteam for asset XXXXX",
  }
}
```
</details>

---


####   POST     - `/asset/{assetId}/admin/create`  

Creates an admin user that is going to be able to authorise other users. Only the asset owner can do this. There can be more than one admin user and the admin can be admin from different assets of different owners.

<u>*Input*</u>
- `assetId` :  `<string>` Unique identifier of the asset.
- `userId` :  `<string>` The user that is going to manage the asset access.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "userId": "did:bteam"
}
```
</details>  
<br>

<u>*Output*</u>
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "message": "Successfully authorised admin user did:vtn:trustid: for asset XX"
  }
}
```
</details>

---



####   POST     - `/asset/{assetId}/admin/authorise`  

Authorise user access for an asset. Only the asset admin can do this.

<u>*Input*</u>
- `assetId` :  `<string>` Unique identifier of the asset.
- `userId` :  `<string>` The authorised user.
- `ownerId` :  `<string>` The asset's owner.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "userId": "did:bteam",
  "ownerId": "did:bteam"
}
```
</details> 
<br>

<u>*Output*</u>
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "message": "Successfully authorised user did:bteam for asset XXXXX",
  }
}
```
</details>

---

####   POST     - `/asset/{assetId}/admin/unauthorise`  

Unauthorise user access for an asset. Only the asset owner can do this.

<u>*Input*</u>
- `assetId` :  `<string>` Unique identifier of the asset.
- `userId` :  `<string>` The unauthorised user.
- `ownerId` :  `<string>` The asset's owner.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "userId": "did:bteam",
  "ownerId": "did:bteam"

}
```
</details>  
<br>

<u>*Output*</u>
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "message": "Successfully unauthorised user did:bteam for asset XXXXX",
  }
}
```
</details>

---

####   POST     - `/asset/{assetId}/admin/delete`  

Delete an admin user that is not going to be able to authorise other users. Only the asset owner can do this. 

<u>*Input*</u>
- `assetId` :  `<string>` Unique identifier of the asset.
- `userId` :  `<string>` The user that is going to manage the asset access.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "userId": "did:bteam"
}
```
</details>  
<br>

<u>*Output*</u>
- `asset`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "output": {
    "message": "Successfully unauthorised admin user did:vtn:trustid: for asset XX"
  }
}
```
</details>

---

####   POST     - `/asset/{assetId}/rules`  

Add rules to monitor asset parameters.

<u>*Input*</u>
- `assetId` :  `<string>` Unique identifier of the asset.
- `rules`:  `<json>` JSON of rules. It can have at least two fields: value & range, to specify a constant value or range of values that has to accomplish a parameter. Every rule (value, range) can contain as many conditions for different parameters as necessary. However it's noted that a use of quite many conditions affects the performance of the asset udpates.

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
  "rules": {
    "value": [
      {
        "param": "a",
        "value": "b"
      },
      {
        "param": "aa",
        "value": "bb"
      }
    ],
    "range": [
      {
        "param": "b",
        "min": 0,
        "max": 100
      }
    ]
  }
}
```
</details> 
<br>

<u>*Output*</u>
- `rules`    :  `<json>` 

<details>
  <summary><em><strong>Sample structure</strong></em> (Click to expand)</summary>

```js
{
{
  "rules": {
    "value": [
      {
        "param": "a",
        "value": "b"
      },
      {
        "param": "aa",
        "value": "bb"
      }
    ],
    "range": [
      {
        "param": "b",
        "min": 0,
        "max": 100
      }
    ]
  }
}
```
</details>

---

#### GET   -    `/assets?isAuthorised=boolean`  

Lists all the assets of a user.

<u>*Input*</u>

- `isAuthorised`: `<boolean>` Flag to get own (false) or authorised (true) assets.

(*) Please navigate to the following [section](#authorised-assets) for isAuthorised query param details.

<u>*Output*</u>
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
The `trustpoint` parameter is only filled in after the creation/registration of a trust point. Thus every new trust point regarding to an asset results in a new transaction in the asset with only the update of this `trustpoint` parameter.

Transaction after creating a trustpoint in HF:

<u>*Output*</u>
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

<u>*Output*</u>
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
 

## How we run the application
As you could see in the [Architecture](architecture.html) module, all the applications are running on cloud. Through Kubernetes orchestration system the application deployment, scaling and management is an easy and automated task.

## Testing the Application
In postman folder there are the collection and environment to interact and test with the API methods. It is only needed to import them into postman application and know to use the coren-trackapi module.

Also you can download the files in the links below:

<a href="_static/trackapi.collection.json" download> - Postman collection</a>
<br>
<a href="_static/environment.json" download> - Postman environment</a>

## Errors management
  
Track API errors are managed through the following JSON:
```
{
  "error": {
    "code": "HTTP status code",
    "function": "function in which the error was generated",
    "message": "error description"
  }
}
```

<br/>