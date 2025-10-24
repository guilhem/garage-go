# Blocks
(*Blocks*)

## Overview

### Available Operations

* [GetInfo](#getinfo) - 
Get detailed information about a data block stored on a Garage node, including all object versions and in-progress multipart uploads that contain a reference to this block.
    
* [ListErrors](#listerrors) - 
List data blocks that are currently in an errored state on one or several Garage nodes.
    
* [Purge](#purge) - 
Purge references to one or several missing data blocks.

This will remove all objects and in-progress multipart uploads that contain the specified data block(s). The objects will be permanently deleted from the buckets in which they appear. Use with caution.
    
* [RetryResync](#retryresync) - 
Instruct Garage node(s) to retry the resynchronization of one or several missing data block(s).
    

## GetInfo


Get detailed information about a data block stored on a Garage node, including all object versions and in-progress multipart uploads that contain a reference to this block.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetBlockInfo" method="post" path="/v2/GetBlockInfo" -->
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

    res, err := s.Blocks.GetInfo(ctx, "<value>", components.LocalGetBlockInfoRequest{
        BlockHash: "<value>",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalGetBlockInfoResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                  | Type                                                                                       | Required                                                                                   | Description                                                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| `ctx`                                                                                      | [context.Context](https://pkg.go.dev/context#Context)                                      | :heavy_check_mark:                                                                         | The context to use for the request.                                                        |
| `node`                                                                                     | *string*                                                                                   | :heavy_check_mark:                                                                         | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request   |
| `localGetBlockInfoRequest`                                                                 | [components.LocalGetBlockInfoRequest](../../models/components/localgetblockinforequest.md) | :heavy_check_mark:                                                                         | N/A                                                                                        |
| `opts`                                                                                     | [][operations.Option](../../models/operations/option.md)                                   | :heavy_minus_sign:                                                                         | The options for this request.                                                              |

### Response

**[*operations.GetBlockInfoResponse](../../models/operations/getblockinforesponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## ListErrors


List data blocks that are currently in an errored state on one or several Garage nodes.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="ListBlockErrors" method="get" path="/v2/ListBlockErrors" -->
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

    res, err := s.Blocks.ListErrors(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalListBlockErrorsResponse != nil {
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

**[*operations.ListBlockErrorsResponse](../../models/operations/listblockerrorsresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Purge


Purge references to one or several missing data blocks.

This will remove all objects and in-progress multipart uploads that contain the specified data block(s). The objects will be permanently deleted from the buckets in which they appear. Use with caution.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="PurgeBlocks" method="post" path="/v2/PurgeBlocks" -->
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

    res, err := s.Blocks.Purge(ctx, "<value>", []string{})
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalPurgeBlocksResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |
| `node`                                                                                   | *string*                                                                                 | :heavy_check_mark:                                                                       | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request |
| `requestBody`                                                                            | []*string*                                                                               | :heavy_check_mark:                                                                       | N/A                                                                                      |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |

### Response

**[*operations.PurgeBlocksResponse](../../models/operations/purgeblocksresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## RetryResync


Instruct Garage node(s) to retry the resynchronization of one or several missing data block(s).
    

### Example Usage

<!-- UsageSnippet language="go" operationID="RetryBlockResync" method="post" path="/v2/RetryBlockResync" -->
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

    res, err := s.Blocks.RetryResync(ctx, "<value>", components.CreateLocalRetryBlockResyncRequestUnionLocalRetryBlockResyncRequest1(
        components.LocalRetryBlockResyncRequest1{
            All: false,
        },
    ))
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalRetryBlockResyncResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                    | Type                                                                                                         | Required                                                                                                     | Description                                                                                                  |
| ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                                        | [context.Context](https://pkg.go.dev/context#Context)                                                        | :heavy_check_mark:                                                                                           | The context to use for the request.                                                                          |
| `node`                                                                                                       | *string*                                                                                                     | :heavy_check_mark:                                                                                           | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request                     |
| `localRetryBlockResyncRequest`                                                                               | [components.LocalRetryBlockResyncRequestUnion](../../models/components/localretryblockresyncrequestunion.md) | :heavy_check_mark:                                                                                           | N/A                                                                                                          |
| `opts`                                                                                                       | [][operations.Option](../../models/operations/option.md)                                                     | :heavy_minus_sign:                                                                                           | The options for this request.                                                                                |

### Response

**[*operations.RetryBlockResyncResponse](../../models/operations/retryblockresyncresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |