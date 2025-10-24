# BucketAliases
(*BucketAliases*)

## Overview

### Available Operations

* [Add](#add) - Add an alias for the target bucket.  This can be either a global or a local alias, depending on which fields are specified.
* [Remove](#remove) - Remove an alias for the target bucket.  This can be either a global or a local alias, depending on which fields are specified.

## Add

Add an alias for the target bucket.  This can be either a global or a local alias, depending on which fields are specified.

### Example Usage

<!-- UsageSnippet language="go" operationID="AddBucketAlias" method="post" path="/v2/AddBucketAlias" -->
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

    res, err := s.BucketAliases.Add(ctx, components.CreateAddBucketAliasRequestUnionAddBucketAliasRequest2(
        components.AddBucketAliasRequest2{
            AccessKeyID: "<id>",
            LocalAlias: "<value>",
            BucketID: "<id>",
        },
    ))
    if err != nil {
        log.Fatal(err)
    }
    if res.AddBucketAliasResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                      | Type                                                                                           | Required                                                                                       | Description                                                                                    |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `ctx`                                                                                          | [context.Context](https://pkg.go.dev/context#Context)                                          | :heavy_check_mark:                                                                             | The context to use for the request.                                                            |
| `request`                                                                                      | [components.AddBucketAliasRequestUnion](../../models/components/addbucketaliasrequestunion.md) | :heavy_check_mark:                                                                             | The request object to use for the request.                                                     |
| `opts`                                                                                         | [][operations.Option](../../models/operations/option.md)                                       | :heavy_minus_sign:                                                                             | The options for this request.                                                                  |

### Response

**[*operations.AddBucketAliasResponse](../../models/operations/addbucketaliasresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Remove

Remove an alias for the target bucket.  This can be either a global or a local alias, depending on which fields are specified.

### Example Usage

<!-- UsageSnippet language="go" operationID="RemoveBucketAlias" method="post" path="/v2/RemoveBucketAlias" -->
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

    res, err := s.BucketAliases.Remove(ctx, components.CreateRemoveBucketAliasRequestUnionRemoveBucketAliasRequest1(
        components.RemoveBucketAliasRequest1{
            GlobalAlias: "<value>",
            BucketID: "<id>",
        },
    ))
    if err != nil {
        log.Fatal(err)
    }
    if res.AddBucketAliasResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                                | :heavy_check_mark:                                                                                   | The context to use for the request.                                                                  |
| `request`                                                                                            | [components.RemoveBucketAliasRequestUnion](../../models/components/removebucketaliasrequestunion.md) | :heavy_check_mark:                                                                                   | The request object to use for the request.                                                           |
| `opts`                                                                                               | [][operations.Option](../../models/operations/option.md)                                             | :heavy_minus_sign:                                                                                   | The options for this request.                                                                        |

### Response

**[*operations.RemoveBucketAliasResponse](../../models/operations/removebucketaliasresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |