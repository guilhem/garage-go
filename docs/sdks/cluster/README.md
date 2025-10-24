# Cluster
(*Cluster*)

## Overview

### Available Operations

* [GetHealth](#gethealth) - Returns the global status of the cluster, the number of connected nodes (over the number of known ones), the number of healthy storage nodes (over the declared ones), and the number of healthy partitions (over the total).
* [GetStatus](#getstatus) - 
Returns the cluster's current status, including:

- ID of the node being queried and its version of the Garage daemon
- Live nodes
- Currently configured cluster layout
- Staged changes to the cluster layout

*Capacity is given in bytes*
    

## GetHealth

Returns the global status of the cluster, the number of connected nodes (over the number of known ones), the number of healthy storage nodes (over the declared ones), and the number of healthy partitions (over the total).

### Example Usage

<!-- UsageSnippet language="go" operationID="GetClusterHealth" method="get" path="/v2/GetClusterHealth" -->
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

    res, err := s.Cluster.GetHealth(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetClusterHealthResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.GetClusterHealthResponse](../../models/operations/getclusterhealthresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetStatus


Returns the cluster's current status, including:

- ID of the node being queried and its version of the Garage daemon
- Live nodes
- Currently configured cluster layout
- Staged changes to the cluster layout

*Capacity is given in bytes*
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetClusterStatus" method="get" path="/v2/GetClusterStatus" -->
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

    res, err := s.Cluster.GetStatus(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetClusterStatusResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.GetClusterStatusResponse](../../models/operations/getclusterstatusresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |