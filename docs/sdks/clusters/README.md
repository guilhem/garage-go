# Clusters
(*Clusters*)

## Overview

### Available Operations

* [ConnectNodes](#connectnodes) - Instructs this Garage node to connect to other Garage nodes at specified `<node_id>@<net_address>`. `node_id` is generated automatically on node start.
* [GetStatistics](#getstatistics) - 
Fetch global cluster statistics.

*Note: do not try to parse the `freeform` field of the response, it is given as a string specifically because its format is not stable.*
    

## ConnectNodes

Instructs this Garage node to connect to other Garage nodes at specified `<node_id>@<net_address>`. `node_id` is generated automatically on node start.

### Example Usage

<!-- UsageSnippet language="go" operationID="ConnectClusterNodes" method="post" path="/v2/ConnectClusterNodes" -->
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

    res, err := s.Clusters.ConnectNodes(ctx, []string{
        "<value 1>",
        "<value 2>",
        "<value 3>",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ConnectClusterNodesResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `request`                                                | [[]string](../../.md)                                    | :heavy_check_mark:                                       | The request object to use for the request.               |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ConnectClusterNodesResponse](../../models/operations/connectclusternodesresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetStatistics


Fetch global cluster statistics.

*Note: do not try to parse the `freeform` field of the response, it is given as a string specifically because its format is not stable.*
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetClusterStatistics" method="get" path="/v2/GetClusterStatistics" -->
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

    res, err := s.Clusters.GetStatistics(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetClusterStatisticsResponse != nil {
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

**[*operations.GetClusterStatisticsResponse](../../models/operations/getclusterstatisticsresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |