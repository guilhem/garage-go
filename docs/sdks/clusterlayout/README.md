# ClusterLayout
(*ClusterLayout*)

## Overview

### Available Operations

* [Apply](#apply) - 
Applies to the cluster the layout changes currently registered as staged layout changes.

*Note: do not try to parse the `message` field of the response, it is given as an array of string specifically because its format is not stable.*
    
* [SkipDeadNodes](#skipdeadnodes) - Force progress in layout update trackers
* [Get](#get) - 
Returns the cluster's current layout, including:

- Currently configured cluster layout
- Staged changes to the cluster layout

*Capacity is given in bytes*
    
* [GetHistory](#gethistory) - 
Returns the history of layouts in the cluster
    
* [PreviewChanges](#previewchanges) - 
Computes a new layout taking into account the staged parameters, and returns it with detailed statistics. The new layout is not applied in the cluster.

*Note: do not try to parse the `message` field of the response, it is given as an array of string specifically because its format is not stable.*
    
* [Revert](#revert) - Clear staged layout changes
* [Update](#update) - 
Send modifications to the cluster layout. These modifications will be included in the staged role changes, visible in subsequent calls of `GET /GetClusterHealth`. Once the set of staged changes is satisfactory, the user may call `POST /ApplyClusterLayout` to apply the changed changes, or `POST /RevertClusterLayout` to clear all of the staged changes in the layout.

Setting the capacity to `null` will configure the node as a gateway.
Otherwise, capacity must be now set in bytes (before Garage 0.9 it was arbitrary weights).
For example to declare 100GB, you must set `capacity: 100000000000`.

Garage uses internally the International System of Units (SI), it assumes that 1kB = 1000 bytes, and displays storage as kB, MB, GB (and not KiB, MiB, GiB that assume 1KiB = 1024 bytes).
    

## Apply


Applies to the cluster the layout changes currently registered as staged layout changes.

*Note: do not try to parse the `message` field of the response, it is given as an array of string specifically because its format is not stable.*
    

### Example Usage

<!-- UsageSnippet language="go" operationID="ApplyClusterLayout" method="post" path="/v2/ApplyClusterLayout" -->
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

    res, err := s.ClusterLayout.Apply(ctx, components.ApplyClusterLayoutRequest{
        Version: 985543,
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ApplyClusterLayoutResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                    | Type                                                                                         | Required                                                                                     | Description                                                                                  |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `ctx`                                                                                        | [context.Context](https://pkg.go.dev/context#Context)                                        | :heavy_check_mark:                                                                           | The context to use for the request.                                                          |
| `request`                                                                                    | [components.ApplyClusterLayoutRequest](../../models/components/applyclusterlayoutrequest.md) | :heavy_check_mark:                                                                           | The request object to use for the request.                                                   |
| `opts`                                                                                       | [][operations.Option](../../models/operations/option.md)                                     | :heavy_minus_sign:                                                                           | The options for this request.                                                                |

### Response

**[*operations.ApplyClusterLayoutResponse](../../models/operations/applyclusterlayoutresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## SkipDeadNodes

Force progress in layout update trackers

### Example Usage

<!-- UsageSnippet language="go" operationID="ClusterLayoutSkipDeadNodes" method="post" path="/v2/ClusterLayoutSkipDeadNodes" -->
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

    res, err := s.ClusterLayout.SkipDeadNodes(ctx, components.ClusterLayoutSkipDeadNodesRequest{
        AllowMissingData: false,
        Version: 530642,
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ClusterLayoutSkipDeadNodesResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                    | Type                                                                                                         | Required                                                                                                     | Description                                                                                                  |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                                        | [context.Context](https://pkg.go.dev/context#Context)                                                        | :heavy_check_mark:                                                                                           | The context to use for the request.                                                                          |
| `request`                                                                                                    | [components.ClusterLayoutSkipDeadNodesRequest](../../models/components/clusterlayoutskipdeadnodesrequest.md) | :heavy_check_mark:                                                                                           | The request object to use for the request.                                                                   |
| `opts`                                                                                                       | [][operations.Option](../../models/operations/option.md)                                                     | :heavy_minus_sign:                                                                                           | The options for this request.                                                                                |

### Response

**[*operations.ClusterLayoutSkipDeadNodesResponse](../../models/operations/clusterlayoutskipdeadnodesresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Get


Returns the cluster's current layout, including:

- Currently configured cluster layout
- Staged changes to the cluster layout

*Capacity is given in bytes*
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetClusterLayout" method="get" path="/v2/GetClusterLayout" -->
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

    res, err := s.ClusterLayout.Get(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetClusterLayoutResponse != nil {
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

**[*operations.GetClusterLayoutResponse](../../models/operations/getclusterlayoutresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetHistory


Returns the history of layouts in the cluster
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetClusterLayoutHistory" method="get" path="/v2/GetClusterLayoutHistory" -->
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

    res, err := s.ClusterLayout.GetHistory(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetClusterLayoutHistoryResponse != nil {
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

**[*operations.GetClusterLayoutHistoryResponse](../../models/operations/getclusterlayouthistoryresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## PreviewChanges


Computes a new layout taking into account the staged parameters, and returns it with detailed statistics. The new layout is not applied in the cluster.

*Note: do not try to parse the `message` field of the response, it is given as an array of string specifically because its format is not stable.*
    

### Example Usage

<!-- UsageSnippet language="go" operationID="PreviewClusterLayoutChanges" method="post" path="/v2/PreviewClusterLayoutChanges" -->
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

    res, err := s.ClusterLayout.PreviewChanges(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.PreviewClusterLayoutChangesResponse != nil {
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

**[*operations.PreviewClusterLayoutChangesResponse](../../models/operations/previewclusterlayoutchangesresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Revert

Clear staged layout changes

### Example Usage

<!-- UsageSnippet language="go" operationID="RevertClusterLayout" method="post" path="/v2/RevertClusterLayout" -->
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

    res, err := s.ClusterLayout.Revert(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetClusterLayoutResponse != nil {
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

**[*operations.RevertClusterLayoutResponse](../../models/operations/revertclusterlayoutresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Update


Send modifications to the cluster layout. These modifications will be included in the staged role changes, visible in subsequent calls of `GET /GetClusterHealth`. Once the set of staged changes is satisfactory, the user may call `POST /ApplyClusterLayout` to apply the changed changes, or `POST /RevertClusterLayout` to clear all of the staged changes in the layout.

Setting the capacity to `null` will configure the node as a gateway.
Otherwise, capacity must be now set in bytes (before Garage 0.9 it was arbitrary weights).
For example to declare 100GB, you must set `capacity: 100000000000`.

Garage uses internally the International System of Units (SI), it assumes that 1kB = 1000 bytes, and displays storage as kB, MB, GB (and not KiB, MiB, GiB that assume 1KiB = 1024 bytes).
    

### Example Usage

<!-- UsageSnippet language="go" operationID="UpdateClusterLayout" method="post" path="/v2/UpdateClusterLayout" -->
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

    res, err := s.ClusterLayout.Update(ctx, components.UpdateClusterLayoutRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.GetClusterLayoutResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                      | Type                                                                                           | Required                                                                                       | Description                                                                                    |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `ctx`                                                                                          | [context.Context](https://pkg.go.dev/context#Context)                                          | :heavy_check_mark:                                                                             | The context to use for the request.                                                            |
| `request`                                                                                      | [components.UpdateClusterLayoutRequest](../../models/components/updateclusterlayoutrequest.md) | :heavy_check_mark:                                                                             | The request object to use for the request.                                                     |
| `opts`                                                                                         | [][operations.Option](../../models/operations/option.md)                                       | :heavy_minus_sign:                                                                             | The options for this request.                                                                  |

### Response

**[*operations.UpdateClusterLayoutResponse](../../models/operations/updateclusterlayoutresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |