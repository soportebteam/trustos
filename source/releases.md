# Releases

TrustOS started with the initial v1.0.0 release. Since that several changes have been implemented in order to improve the functionality and performance of each API. Take a look at the last changes.

## Track API

<details><summary> v2.0.0 [June 2020]</summary><hr>

**What's new in Track API v2.0.0:**

- Compatibility with Hyperledger Fabric v2.x.x
- Integration with TrustID (ID API) for interacting with the network and offer basic identity management services to users (create, import, export verify and sign)
- The Track chaincode (smart contract in Hyperledger Fabric) is now deployed as external services. It makes possible to deploy, handle and upgrade as an external container in a simple and fast way.

**Changes, fixes and deprecations:**

- The model of user credentials (user, password) used for `/login` method is now used with did credentials (id, password)
- Current user credentials are and looks like a DID credential: `did:vtn:trustid:289f893a9oir930pajklbx938ajzhd87as7893` instead of: `user:org1MSP`
- The internal functions of invoking / querying a service (chaincode) are changed to new service model managed by TrustID
- Some minor fixes regarding API's HTTP response status code (2xx successful, 4xx client error, 5xx server error)

</details>

<details><summary> v1.1.0 [April 2020]</summary><hr>

**What's new in Track API v1.1.0:**

- New trustpoint param in the Asset data model for grouping and showing information about trust points. Every call to createTrust or registerTrust functions (that is the creation/registration of the trust point in Hyperledger Fabric/Ethereum) involves an update of the trustpoint param in the asset. So this way allows to know when/where the trust point was generated.
- In order to increase the performance every update of the asset is now done in a separated and independent manner, so it doesn't keep the last state, just the asset data that is immutable. (f.e. when there is a creation/registration of a trustpoint, the new transaction just fill the trustpoint field, but not the metadata contained in the last asset transaction)
- News in Swagger UI: link to Readthedocs and data model section with proper nomenclature
- New `/refresh` method to able to refresh the JWT TOKEN without having to write again the user credentials

**Changes, fixes and deprecations:**

- The history/range of asset transactions now returns an array of txs also when there is only 1 transaction.
- The history/range of asset transaction is now returned from newest to oldest
- Postman collections are now updated
</details>

<details><summary> v1.0.0 [December 2019]</summary><hr>

**What's new in Track API v1.0.0:**

- All basic tracking functionalities working: create, manage, and export digital assets on the blockchain
- API visualisation and interaction through Swagger UI
- Common errors management method implemented
- API integration testing with Hyperledger Fabric. Already successfully integrated with Hyperledger Fabric SDK and network and deployed through Kubernetes system with continuous integration and continuous deployment (CICD) mechanisms.

**Changes, fixes and deprecations:**

- All issues from previous releases (< v1.0.0) are solved and closed 
- API code is cleaned and improved and unnecessary files are removed from the repository
- Third party dependencies are handled through Go modules 

</details><br>

## Token API

<details><summary> v2.0.0 [June 2020]</summary><hr>

**What's new in Token API v2.0.0:**

- Compatibility with Hyperledger Fabric v2.x.x
- Integration with TrustID (ID API) for interacting with the network and offer basic identity management services to users (create, import, export verify and sign)
- The Token chaincode (smart contract in Hyperledger Fabric) is now deployed as external services. It makes possible to deploy, handle and upgrade as an external container in a simple and fast way.

**Changes, fixes and deprecations:**
- Owner of a token automatically set from the transaction issuer. Removed manual set of owner in `/create`
- The model of user credentials (user, password) used for `/login` method is now used with did credentials (id, password)
- Current user credentials are and looks like a DID credential: `did:vtn:trustid:289f893a9oir930pajklbx938ajzhd87as7893` instead of: `user:org1MSP`
- The internal functions of invoking / querying a service (chaincode) are changed to new service model managed by TrustID
- Some minor fixes regarding API's HTTP response status code (2xx successful, 4xx client error, 5xx server error)

</details>

<details><summary> v1.1.0 [March 2020]</summary><hr>

**What's new in Token API v1.1.0:**

- New token data model: a single chaincode can handle multiple tokens. Since the creation of a new token incurs sometimes in a timeout response error because of the process time while installing and instantiating a new chaincode, there was a need to implement a new data model based on a one single chaincode
- News in Swagger UI: link to Readthedocs and data model section with proper nomenclature
- New `/refresh` method to able to refresh the JWT TOKEN without having to write again the user credentials

**Changes, fixes and deprecations:**

- Changes in the implementation for `/token/{id}/transactions` path. Now it is allowed that a token owner can get the transactions of specific user in the way `/token/{id}/transactions?userId="test"`
- The paths `/token/initialize` and `/token/instantiate` are converged in `/token/create`
- Postman collections are now updated

</details>

<details><summary> v1.0.1 [January 2020]</summary><hr>

**What's new in Token API v1.0.1:**

- Improvement based on writes performance. Now the token balances are handled separately as same way as the token information defined in the creation. Each one of the token transaction (f.e. token transfer transaction) are written in a separately way using completely different composite keys based on the user.

**Changes, fixes and deprecations:**

- FIXED: Known vulnerability that makes possible to upgrade the token replacing the token information defined in its creation.
- DEPRECATED: token implementation based on a unique token state which contains all the balances and token information in a unique key. It was deprecated because of the low performance.

</details>

<details><summary> v1.0.0 [December 2019]</summary><hr>

**What's new in Token API v1.0.0:**

- All basic token functionalities working: 
- API visualisation and interaction through Swagger UI
- Common errors management method implemented
- API integration testing with Hyperledger Fabric. Already successfully integrated with Hyperledger Fabric SDK and network and deployed through Kubernetes system with continuous integration and continuous deployment (CICD) mechanisms.

**Changes, fixes and deprecations:**

- All issues from previous releases (< v1.0.0) are solved and closed 
- API code is cleaned and improved and unnecessary files are removed from the repository
- Third party dependencies are handled through Go modules 

</details><br>

## Settle API

<details><summary> v2.0.0 [June 2020]</summary><hr>

**What's new in Settle API v2.0.0:**

- Compatibility with Hyperledger Fabric v2.x.x
- Integration with TrustID (ID API) for interacting with the network and offer basic identity management services to users (create, import, export verify and sign)
- The Settle chaincode (smart contract in Hyperledger Fabric) is now deployed as external services. It makes possible to deploy, handle and upgrade as an external container in a simple and fast way.

**Changes, fixes and deprecations:**

- The model of user credentials (user, password) used for `/login` method is now used with did credentials (id, password)
- Current user credentials are and looks like a DID credential: `did:vtn:trustid:289f893a9oir930pajklbx938ajzhd87as7893` instead of: `user:org1MSP`
- The internal functions of invoking / querying a service (chaincode) are changed to new service model managed by TrustID
- Some minor fixes regarding API's HTTP response status code (2xx successful, 4xx client error, 5xx server error)

</details>

<details><summary> v1.1.0 [April 2020]</summary><hr>

**What's new in Settle API v1.1.0:**

- In order to increase the performance every update of the settlement with record is now done in a separated and independent way through composite keys implementation
- New `/settlement/{id}/global` function to get global status of the settlement structure. 
- New `/refresh` method to able to refresh the JWT TOKEN without having to write again the user credentials

**Changes, fixes and deprecations:**
- Splitted get settlement structure function into get status for the logged user and get global status.
- The function for getting the global status `/settlement/{id}` only gets the status for the logged user.
- Postman collections are now updated


</details>

<details><summary> v1.0.0 [December 2019]</summary><hr>

**What's new in Settle API v1.0.0:**

- All basic settlement functionalities working: create, update, aggregate, and settle a settlement structure on the blockchain
- API visualisation and interaction through Swagger UI
- Ensuring the transparency through hash and merkle tree mechanisms
- Common errors management method implemented
- API integration testing with Hyperledger Fabric. Already successfully integrated with Hyperledger Fabric SDK and network and deployed through Kubernetes system with continuous integration and continuous deployment (CICD) mechanisms.

**Changes, fixes and deprecations:**

- All issues from previous releases (< v1.0.0) are solved and closed 
- API code is cleaned and improved and unnecessary files are removed from the repository
- Third party dependencies are handled through Go modules 

</details><br>

## Trust API

<details><summary> v2.0.0 [June 2020]</summary><hr>

**What's new in Trust API v2.0.0:**

- Compatibility with Hyperledger Fabric v2.x.x
- Integration with TrustID (ID API) for interacting with the network and offer basic identity management services to users (create, import, export verify and sign)
- Some minor fixes regarding API's HTTP response status code (2xx successful, 4xx client error, 5xx server error)
- The Trust chaincode (smart contract in Hyperledger Fabric) is now deployed as external services. It makes possible to deploy, handle and upgrade as an external container in a simple and fast way.

**Changes, fixes and deprecations:**

- New body input field in `/register`and `/create` methods to allow to fill the asset's metadata once the /registration/creation of a trustpoint is done and the asset is updated with the trustpoint info (ethereum transaction & contract or hyperledger fabric transaction) 
- The model of user credentials (user, password) used for `/login` method is now used with did credentials (id, password)
-  Current user credentials are and looks like a DID credential: `did:vtn:trustid:289f893a9oir930pajklbx938ajzhd87as7893` instead of: `user:org1MSP`
- The internal functions of invoking / querying a service (chaincode) are changed to new service model managed by TrustID

</details>

<details><summary> v1.0.0 [December 2019]</summary><hr>

**What's new in Trust API v1.0.0:**

- All basic trust functionalities working: create, manage and public register trust points
- API visualisation and interaction through Swagger UI
- Ensuring the transparency through hash and merkle tree mechanisms
- Common errors management method implemented
- API integration testing with Hyperledger Fabric. Already successfully integrated with Hyperledger Fabric SDK and network and deployed through Kubernetes system with continuous integration and continuous deployment (CICD) mechanisms.

**Changes, fixes and deprecations:**

- All issues from previous releases (< v1.0.0) are solved and closed 
- API code is cleaned and improved and unnecessary files are removed from the repository
- Third party dependencies are handled through Go modules 

</details><br>


