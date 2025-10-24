# Permissions
(*Permissions*)

## Overview

### Available Operations

* [AllowBucketKey](#allowbucketkey) - 
⚠️ **DISCLAIMER**: Garage's developers are aware that this endpoint has an unconventional semantic. Be extra careful when implementing it, its behavior is not obvious.

Allows a key to do read/write/owner operations on a bucket.

Flags in permissions which have the value true will be activated. Other flags will remain unchanged (ie. they will keep their internal value).

For example, if you set read to true, the key will be allowed to read the bucket.
If you set it to false, the key will keeps its previous read permission.
If you want to disallow read for the key, check the DenyBucketKey operation.
    
* [DenyBucketKey](#denybucketkey) - 
⚠️ **DISCLAIMER**: Garage's developers are aware that this endpoint has an unconventional semantic. Be extra careful when implementing it, its behavior is not obvious.

Denies a key from doing read/write/owner operations on a bucket.

Flags in permissions which have the value true will be deactivated. Other flags will remain unchanged.

For example, if you set read to true, the key will be denied from reading.
If you set read to false,  the key will keep its previous permissions.
If you want the key to have the reading permission, check the AllowBucketKey operation.
    

## AllowBucketKey


⚠️ **DISCLAIMER**: Garage's developers are aware that this endpoint has an unconventional semantic. Be extra careful when implementing it, its behavior is not obvious.

Allows a key to do read/write/owner operations on a bucket.

Flags in permissions which have the value true will be activated. Other flags will remain unchanged (ie. they will keep their internal value).

For example, if you set read to true, the key will be allowed to read the bucket.
If you set it to false, the key will keeps its previous read permission.
If you want to disallow read for the key, check the DenyBucketKey operation.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="AllowBucketKey" method="post" path="/v2/AllowBucketKey" -->
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

    res, err := s.Permissions.AllowBucketKey(ctx, components.AllowBucketKeyRequest{
        AccessKeyID: "<id>",
        BucketID: "<id>",
        Permissions: components.APIBucketKeyPerm{},
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.AddBucketAliasResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                            | Type                                                                                 | Required                                                                             | Description                                                                          |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `ctx`                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                | :heavy_check_mark:                                                                   | The context to use for the request.                                                  |
| `request`                                                                            | [components.AllowBucketKeyRequest](../../models/components/allowbucketkeyrequest.md) | :heavy_check_mark:                                                                   | The request object to use for the request.                                           |
| `opts`                                                                               | [][operations.Option](../../models/operations/option.md)                             | :heavy_minus_sign:                                                                   | The options for this request.                                                        |

### Response

**[*operations.AllowBucketKeyResponse](../../models/operations/allowbucketkeyresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## DenyBucketKey


⚠️ **DISCLAIMER**: Garage's developers are aware that this endpoint has an unconventional semantic. Be extra careful when implementing it, its behavior is not obvious.

Denies a key from doing read/write/owner operations on a bucket.

Flags in permissions which have the value true will be deactivated. Other flags will remain unchanged.

For example, if you set read to true, the key will be denied from reading.
If you set read to false,  the key will keep its previous permissions.
If you want the key to have the reading permission, check the AllowBucketKey operation.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="DenyBucketKey" method="post" path="/v2/DenyBucketKey" -->
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

    res, err := s.Permissions.DenyBucketKey(ctx, components.AllowBucketKeyRequest{
        AccessKeyID: "<id>",
        BucketID: "<id>",
        Permissions: components.APIBucketKeyPerm{},
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.AddBucketAliasResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                            | Type                                                                                 | Required                                                                             | Description                                                                          |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `ctx`                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                | :heavy_check_mark:                                                                   | The context to use for the request.                                                  |
| `request`                                                                            | [components.AllowBucketKeyRequest](../../models/components/allowbucketkeyrequest.md) | :heavy_check_mark:                                                                   | The request object to use for the request.                                           |
| `opts`                                                                               | [][operations.Option](../../models/operations/option.md)                             | :heavy_minus_sign:                                                                   | The options for this request.                                                        |

### Response

**[*operations.DenyBucketKeyResponse](../../models/operations/denybucketkeyresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |