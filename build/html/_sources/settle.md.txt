
# Settle

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
<br>

### Methods

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
    <td class="tg-0pky">SETTLE-00</td>
    <td class="tg-0pky">Service is down</td>
  </tr>
  <tr>
    <td class="tg-0pky">SETTLE-01</td>
    <td class="tg-0pky">Error parsing any data structure</td>
  </tr>
  <tr>
    <td class="tg-0lax">SETTLE-02</td>
    <td class="tg-0lax">Error of some kind of functionality</td>
  </tr>
</table>