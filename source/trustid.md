
# TrustID
 
TrustID is a standalone identity module for TrustOS. We followed a decentralized identity approach for its design, where users (and services) are identified through a DID. 

TrustID is an opensource project and it was released as an opensource project under the umbrella of the Hyperledger Labs.

These DIDs follow the W3C standard, and they serve as a unique ID to identify users. DIDs aggregate all the pieces of public information required to authenticate a user (i.e., their public key or X.509 certificate).

This is the structure of a DID Identity:

- `id` :  `<string>` Unique identifier of the identity using the W3C standard.
- `pubkey` :  `<String>` Public key of the identity.
- `privkey` :  `<string>` Private key of the identity.
- `type` :  `<string>` Algorithm used in order to generate the keys.
- `controller` :  `<String>` Verifier of the identity. In future, an identity should have more than one controller.

Example:
````
{
  "id": "did:vtn:trustid:d830c50977703f421a0ed5a8707ecfe50559fe73dd2bf90c261b76a1379acbea",
  "type": "RSA",
  "controller": "",
  "access": 0,
  "privkey": "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",
  "pubkey": "-----BEGIN PUBLIC KEY-----\r\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxfun1NH3jOlNRuX0z7cr\r\n5eFWCt/xUSKwikYg7NRoaNn/NNAQln/BDSamVG3RwlmM/dvUt783Hp7YqeHscXmp\r\ngKwWiF/RycT3Sx9l3qC0MfLlbmsQJ0ZqO+Iuy+vjAxq4RGTS1dzuCjipPy4yBCxB\r\nrWT/q3lFboWaEAoFA+DFm0Hwt47P+lApAfcMc0JduW31gaULUNpqTZyQJBwBKfk1\r\nBZPrurutwnEuOxOOOFNXXL/IUSqneC+71drGO4xA1Sq1bKtsJE9WYW3U8w4C8dHs\r\nU1rq9z/MOAsUlz+DGzyIMI16ypjTC8T4BkWg9vGPgf/C8ropgsbx+9fMKBSisHG5\r\ntQIDAQAB\r\n-----END PUBLIC KEY-----\r\n"
}
````

This is the structure that is stored in the DLT platform that belongs to an user or device identity:

- `Did` :  `<string>` Unique identifier of the identity using the W3C standard.
- `PubKey` :  `<String>` Public key of the identity.
- `Controller` :  `<String>` Verifier of the identity. In future, an identity should have more than one controller.
- `Access` :  `<integer>` Policy of the identity in order of identity operations, 0 root, 1 admin, 2 user.

Example
````
{
  "Did  ": "did:vtn:trustid:d830c50977703f421a0ed5a8707ecfe50559fe73dd2bf90c261b76a1379acbea",
  "Controller": "",
  "Access": 0, 
  "PubKey": "-----BEGIN PUBLIC KEY-----\r\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxfun1NH3jOlNRuX0z7cr\r\n5eFWCt/xUSKwikYg7NRoaNn/NNAQln/BDSamVG3RwlmM/dvUt783Hp7YqeHscXmp\r\ngKwWiF/RycT3Sx9l3qC0MfLlbmsQJ0ZqO+Iuy+vjAxq4RGTS1dzuCjipPy4yBCxB\r\nrWT/q3lFboWaEAoFA+DFm0Hwt47P+lApAfcMc0JduW31gaULUNpqTZyQJBwBKfk1\r\nBZPrurutwnEuOxOOOFNXXL/IUSqneC+71drGO4xA1Sq1bKtsJE9WYW3U8w4C8dHs\r\nU1rq9z/MOAsUlz+DGzyIMI16ypjTC8T4BkWg9vGPgf/C8ropgsbx+9fMKBSisHG5\r\ntQIDAQAB\r\n-----END PUBLIC KEY-----\r\n"
}
````

This is the structure of a service identity:


- `serviceID` :  `<string>` Unique identifier for the service.
- `Name` :  `<string>` Chaincode or smart contract identifier at the DLT level.
- `Controller` :  `<string>` Owner/admin of the service.
- `Access` :  `<string>` Access policy to the service.
- `Channel` :  `<string>` Network ID of the service.

Example: 

```
{
  "serviceID":  "track",
  "name": "trackscc",
  "access": {
  	"policy": "PUBLIC"
  },
  "channel": "telefonicachannel"
}
```

In order to uniquely identify chaincodes and services deployed in TrustOS, we decided to also give them DIDs so that they could be seamlessly discovered and accessed even if they "live" in independent channels not shared by all the organizations of the network. 

All the authentication and management of identities in the system is performed on-chain through an "Identity Chaincode".

If user A wants to start interacting with the network, he requests the generation of a new DID. The related keys to this DID could be an existing X.509 issued by a valid organization, or even an Ethereum-related public key (internally we use all the JWS, JWE, JWK, secp256k1, etc. RFCs to make our Fabric infrastructure compatible with identities of any nature for the sake of interoperability). This DID generation request has to be validated by a valid organization of the network. Once verified, every transaction signed by user A and directed through a Proxy chaincode is authenticated successfully and delegated to the corresponding chaincode.

![TrustID Flow](./images/trustid-flow.png)

The TrustID project is conformed by the aforementioned chaincode and a client SDK to ease the integration and interaction with TrustID-enabled networks.

TrustID is designed to ease the management of identities for the case of TrustOS. Users shouldn’t need to hold a different set of credentials for each network or decentralized application they interact with. The same credentials used to access your owned Bitcoins and manage your tokens in Ethereum should let you update the state of a Fabric asset or launch a secondary market in TrustOS.


## TrustID SDK

This SDK exposes all the functionalities required to interact with TrustID-based DLT networks. 

### Install
* To install this library you need access to the private repo:
```
npm install trustos-trustid-sdk
```

### Structure
The library has the following modules:

#### Wallet

* `wallet.ts`: Core module of the library. It wraps all the state and logic for identity management and interaction with TrustID networks. To start using the SDK a new wallet needs to be initialized. A wallet exposes the following methods:
    * `setKeystore(keystore: Keystore): void`: Sets a type of keystore, supported: in memory, filesystem, mongodb.
    * `generateDID(type: string, controller: string, passphrase): DID`: Generates an identity.
    * ` storeDID(did: DID): Promise<boolean>`: Stores the did in the keystore.
    * `updateDID(did: DID): Promise<boolean> `: Updates info from DID.
    * `listDID(): string[]`: Returns dids stored in keystore.
    * `recoverKeySSS(id: string, secrets: Buffer[], newPassword: string): Promise<void>`: Recovers the key.
    * `updatePassword(id: string, oldPassphrase:,passphrase: string=""): Promise<void> `: Updates the password to unlock the did.
    * `updateTempKeyDID(id: string, passphrase:,tempPassphrase: string=""): Promise<void>`: Unlocks the account with a temporal key.
    * `addNetwork(id: string, network: TrustID): void`: Adds a new network to interact to.
    

#### Class DID
* `class DID`: Has the following structure:
  * `id: string`: Id string that identifies the DID.
  * `pubkey: string`: PublicKey of the DID.
  * `type: string`: Key type (RSA / EC / OKP).
  * `controller: string`: Verifier of the identity.
  * `access: number`: Access level.
  * `private privkey: string`: Private Key of the DID.
  * `private recoveryKey: string`: Private Key to recover the DID.

And exposes the following functions:
  * `unlockAccount(passphrase: string): void`: Unlocks private key in order to use the DID.
  * `unlockAccountTemp(passphrase: string): void`: Unlocks private key with a temporal key in order to use the DID.
  * `lockAccount(): any`: Locks the private key for a DID.
  * `sign(payload: object, passphrase: string): string`: Sign a payload with a specific DID.
  * `verify(signature: string, id: string): any`: Verifies a signature from a DID.
  * `updatePassword(oldPassphrase:, passphrase:): Promise < DID >`: Updates the password.
  * `generateRecoveryKey(password:string, shares: number, threshold: number): Promise <Buffer[]>`: Generates the recovery key using shamirs secrets sharing.
  * `generateRecoveryKeyTemp(passwordTemp:string, shares: number, threshold: number): Promise <Buffer[]>`: Generates the recovery key using shamirs secrets sharing unlocking the account with the temporal Key.
  * `recoverKey(secrets: Buffer[], newPassword: string): Promise < DID >`: Recovers the key using the secrets generated with Shamirs secrets sharing algorithm.
  * `exportDID(withPrivate: boolean)` : Exports a Did stored in the keystore.
  * `importDID(obj: any)`: Imports a DID and stores it in the keystore.
  * `sign(payload: object): Promise < string >`: Generates a JWS from a payload using an id from the wallet.
  * `verify(signature: string, did: DID): Promise < any > `: Verifies a JWS from a payload using a did.

#### TrustID operations

* `TrustID.ts`: Interface that enables the inteoperation  between the drivers and the different  functionalities of TrustID. The only component implemented currently is the `trustIDhf.ts` enabling the interaction with Hyperledger Fabric TrustID.
networks.
  * `configureDriver(endpoint: string): void`: Sets the network endpoint to interact with the TrustID network.
  * `disconnectDriver(endpoint: string): void`: Disconects the network endpoint to interact with the TrustID network.
  * `createIdentity(did: DID): Promise<object>`: Create an identity in TrustID. It generates a new DID in the wallet and register it in the network.
  * `importIdentity(did: DID, controller?: DID)`: Imports an existing identity to the chaincode.
  * `verifyIdentity(adminDID: DID, id:string): Promise<object>`: Verifies an identity as an admin.
  * `getIdentity(did: DID, id: string): Promise<object>`: Gets a registered identity from TrustID.
  * `revokeIdentity(adminDID: DID, id: string): Promise<object>`: Revokes a registered identity. Only supported by the owner or controller of the DID.
  * `createService(did: DID, serviceDID: string, name: string, isPublic: boolean): Promise<object>`: Creates a new service in the TrustID network.
  * `updateService(did: DID, serviceDID: string, access: Access, isPublic: boolean): Promise<object>`: Updates the information from a service.
  * `updateServiceAccess(did: DID, serviceDID: string, access: AccessPolicy): Promise<object>`: Updates the access from a service.
  * `getService(did: DID, serviceDID: string): Promise<object>`: Gets information from a registered service.
  * `invoke (did: DID, serviceDID: string, args: string[], channel: string): Promise<object>`: Invokes a function of a registered service in the TrustID network.
  * `query(did: DID, serviceDID: string, args: string[], channel: string): Promise<object>`: Queries a function of a registered service in the TrustID network.
 * `PolicyType (policy: PolicyType, threshold:?Number, registry:?object)`: It
    defined the policyType to be used for a service. There are currently three
    types of policyTypes supported (more could be easily added according to
    your needs)
        * PublicPolicy: Grants public access by any user to your service.
        * SameControllerPolicy: Only verified identities whose controller is the
        same controller who created the service has access to the service (this
        policy comes pretty handy when you want to define "corporate-wide" services).
        * FineGrainedPolicy: Grants fine-grained access to users to your service.
        In this policy you explicitly define the access of users to the service.
        There are two ways of using this policyType, you can define a threshold
        so every user with an access level equal or higher than the threshold
        is granted access to the service; or you could use fine-grained
        access levels defined in the registry, where you would add the following
        tuple: `{<did>, <access_role>}`. Thus, only users in the registry 
        with an access level over the threshold will be granted access to the
        service with `access_role` permissions.

#### Driver operations

* `driver.ts`: Interface that enables the implementation of connection drivers with different TrustID networks. The only driver implemented currently is the `hfdriver.ts` enabling the interaction with Hyperledger Fabric TrustID networks.

  * `connect(config: object): Promise<object>;`: Connects with a DLT networks.
  * `disconnect(config: object): void`: Disconnects of a DLT network.
  * `checkConnection(channelName?:string): Promise<object>`: Check the connection with a DLT.
  *  `callContractTransaction(id: string, fcn: string, args: any, channel?: string): Promise<object>`: Write operation in the DLT.
  *  `getContractTransaction(id: string, fcn: string, args: any, channel?: string): Promise<object>`: Read operation in the DLT.

#### Keystore

* `keystore.ts`: Interface that enables the implementation of keystore storages.bThere are currently two implementations of keystore supported: `FileKeystore.ts` (to store DIDs in file keystore)and `MongoKeystore.ts` (to store DIDs in MongoDB).
    * `abstract getDID(id: string): DID`: It gets specific DID from keystore.
    * `abstract storeDID(did: DID): boolean`: It stores DID in keystore.
    * `abstract updateDID(did: DID): boolean`: It updates DID in keystore.
    * `storeInMemory(did: DID): boolean`: Stores DID inMemory for easy and performant use.
    * `listDID(): string[]`: List DIDs in memory.
    * `setDefault(did: DID): boolean`: Set DID as default identity for the keystore wallet.


If you want additional information of TrustID, its SDK and its functionality check the following [repo](https://github.com/hyperledger-labs/TrustID).


### Example of use
```js
// Use library
var id = require('trustos-trustid-sdk')
import { Keystore } from './keystore/keystore';

// Initialize wallet
wal = id.Wallet.Instance;

// Initialize new FileKeystore with storage at ./keystore
const ks = new sdk.FileKeystore("file", "./keystore");
wal.setKeystore(ks)
// ccp is the configu file of a Hyperledger Fabric network
const ccp = JSON.parse(fs.readFileSync("../ccp-dev-dsn.json", 'utf8'));
const config = { // additional config to connect with hyperledger fabric
    stateStore: '/tmp/statestore',
    caURL: 'https://ca:7054',
    caName: 'ca',
    caAdmin: 'admin',
    caPassword: 'password',
    tlsOptions: {
        trustedRoots: "Certificate",
        verify: false
    },
    mspId: 'telefonicaMSP',
    walletID: 'admin',
    asLocalhost: false,
    ccp: ccp,
    chaincodeName: "identitycc", //name of the trustid contract deployed on fabric
    fcn: "proxy",
    channel: "channel1"
}


// Create HF driver to interact with a hyperledger fabric network
var trustID = new sdk.TrustIdHf(config);
// Add and configure the network driver in our wallet.
wal.addNetwork("hf", trustID);
await wal.networks["hf"].configureDriver()

// IDENTITY OPERATION
 // Generate key pair locally.
const did = await wal.generateDID("RSA", "test", "test")
await did.unlockAccount("test")
    // Register in the platform.
await wal.networks.hf.createSelfIdentity(did)
 wal.setDefault(did)
// Get the registered identity.
let res = await wal.networks.hf.getIdentity(did, did.id)
console.log("[*] Get registered identity\n", res)

//SERVICES OPERATIONS
await wal.networks.hf.createService(did, "coren-trackscc", "track", "PUBLIC", "channel1")

let res = await wal.networks.hf.getService(did, "coren-trackscc")
// Create an asset in the service: Track operation via trustid
const asset = {assetId: "test"+Date.now(), data:{"a":1, "b":2}, metadata: {"c": 4}}
const assetStr = JSON.stringify(asset)
// Invoke tract
res = await wal.networks.hf.invoke(did, "coren-trackscc",["createAsset", assetStr], "channel1")
console.log("[*] Asset creation:\n", res)
    // Get the created asset.
res = await wal.networks.hf.invoke(did, "coren-trackscc",["getAsset", JSON.stringify({assetId: asset.assetId})], "channel1")
console.log("[*] Asset registered\n", res)

```
<hr>



## Roadmap
- TrustID compatible with Hyperledger Indy, Verifiable Credentials, etc.
- Anonymous authentication with anonymous transactions.
- Integration with other Identity Providers, related with the non-blockchain world.
- Support for other Keys algorithms, now only RSA is supported.
- Compatibility with Ethereum keys.
