# Token

Token API allows developers to easily create, transfer and get transferable tokens on the Hyperledger Fabric network. Through this API giving transferable value to simple assets can generate new markets and gamification strategies.

## API Specification

An abstraction API with all the token functionalities.

### Token

A token is an asset that gets a transferable value on the blockchain network and can represent whatever it can be imagined, either an abstract or real/physic thing. The term is a little bit confusing at first, since a token can represent the whole class, in which the total supply is declarated, or individual tokens (balances) transferable between users.

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
<br>

### Methods

![TokenAPI methods](./images/token_swagger.png)


<details>
  <summary><em><strong>Token methods</strong></em> (Click to expand)</summary>

---

#### POST   -   `/token/create`

Initialize a new token in the network with some specific information

*Input*
- `name` :  `<string>` Name of the token
- `symbol` : `<string>` Shortname of the token
- `owner` :  `identifier<string>:company<string>` Owner of the token contract
- `ethereumAddress` :  `<string>` This address represents the smart contract in Ethereum associated to the token. At the moment is given as an input, but in future releases it will be created by the chaincode and given to the developer as a response 
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

#### GET   -   `/token/{tokenId}`

Gets all the token information

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
<br>

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

Also you can download the files in the links below:

<a href="_static/tokenapi.collection.json" download> - Postman collection</a>
<br>
<a href="_static/environment.json" download> - Postman environment</a>


## Errors management
  
  Token API errors are managed through the following nomenclature **TOKEN-XX** which corresponds to:<br>


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
    <td class="tg-0pky">TOKEN-00</td>
    <td class="tg-0pky">Service is down</td>
  </tr>
  <tr>
    <td class="tg-0pky">TOKEN-01</td>
    <td class="tg-0pky">Error parsing any data structure</td>
  </tr>
  <tr>
    <td class="tg-0lax">TOKEN-02</td>
    <td class="tg-0lax">Error of some kind of functionality</td>
  </tr>
</table>

<br>