# Nodes
(*Nodes*)

## Overview

### Available Operations

* [CreateMetadataSnapshot](#createmetadatasnapshot) - 
Instruct one or several nodes to take a snapshot of their metadata databases.
    
* [GetInfo](#getinfo) - 
Return information about the Garage daemon running on one or several nodes.
    
* [GetStatistics](#getstatistics) - 
Fetch statistics for one or several Garage nodes.

*Note: do not try to parse the `freeform` field of the response, it is given as a string specifically because its format is not stable.*
    
* [LaunchRepairOperation](#launchrepairoperation) - 
Launch a repair operation on one or several cluster nodes.
    

## CreateMetadataSnapshot


Instruct one or several nodes to take a snapshot of their metadata databases.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="CreateMetadataSnapshot" method="post" path="/v2/CreateMetadataSnapshot" -->
```go
package main

import(
	"context"
	garage "github.com/guilhem/garage-go"
	"log"
)

func main() {
    ctx := context.Background()

    s := garage.New()

    res, err := s.Nodes.CreateMetadataSnapshot(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalCreateMetadataSnapshotResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |
| `node`                                                                                   | *string*                                                                                 | :heavy_check_mark:                                                                       | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |

### Response

**[*operations.CreateMetadataSnapshotResponse](../../models/operations/createmetadatasnapshotresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetInfo


Return information about the Garage daemon running on one or several nodes.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetNodeInfo" method="get" path="/v2/GetNodeInfo" -->
```go
package main

import(
	"context"
	garage "github.com/guilhem/garage-go"
	"log"
)

func main() {
    ctx := context.Background()

    s := garage.New()

    res, err := s.Nodes.GetInfo(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalGetNodeInfoResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |
| `node`                                                                                   | *string*                                                                                 | :heavy_check_mark:                                                                       | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |

### Response

**[*operations.GetNodeInfoResponse](../../models/operations/getnodeinforesponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetStatistics


Fetch statistics for one or several Garage nodes.

*Note: do not try to parse the `freeform` field of the response, it is given as a string specifically because its format is not stable.*
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetNodeStatistics" method="get" path="/v2/GetNodeStatistics" -->
```go
package main

import(
	"context"
	garage "github.com/guilhem/garage-go"
	"log"
)

func main() {
    ctx := context.Background()

    s := garage.New()

    res, err := s.Nodes.GetStatistics(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalGetNodeStatisticsResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |
| `node`                                                                                   | *string*                                                                                 | :heavy_check_mark:                                                                       | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |

### Response

**[*operations.GetNodeStatisticsResponse](../../models/operations/getnodestatisticsresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## LaunchRepairOperation


Launch a repair operation on one or several cluster nodes.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="LaunchRepairOperation" method="post" path="/v2/LaunchRepairOperation" -->
```go
package main

import(
	"context"
	garage "github.com/guilhem/garage-go"
	"github.com/guilhem/garage-go/models/components"
	"log"
)

func main() {
    ctx := context.Background()

    s := garage.New()

    res, err := s.Nodes.LaunchRepairOperation(ctx, "<value>", components.LocalLaunchRepairOperationRequest{
        RepairType: components.CreateRepairTypeUnionRepairTypeTables(
            components.RepairTypeTablesTables,
        ),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalLaunchRepairOperationResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                    | Type                                                                                                         | Required                                                                                                     | Description                                                                                                  |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                                        | [context.Context](https://pkg.go.dev/context#Context)                                                        | :heavy_check_mark:                                                                                           | The context to use for the request.                                                                          |
| `node`                                                                                                       | *string*                                                                                                     | :heavy_check_mark:                                                                                           | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request                     |
| `localLaunchRepairOperationRequest`                                                                          | [components.LocalLaunchRepairOperationRequest](../../models/components/locallaunchrepairoperationrequest.md) | :heavy_check_mark:                                                                                           | N/A                                                                                                          |
| `opts`                                                                                                       | [][operations.Option](../../models/operations/option.md)                                                     | :heavy_minus_sign:                                                                                           | The options for this request.                                                                                |

### Response

**[*operations.LaunchRepairOperationResponse](../../models/operations/launchrepairoperationresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |