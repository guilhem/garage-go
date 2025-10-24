# AccessKeys
(*AccessKeys*)

## Overview

### Available Operations

* [Create](#create) - Creates a new API access key.
* [Delete](#delete) - Delete a key from the cluster. Its access will be removed from all the buckets. Buckets are not automatically deleted and can be dangling. You should manually delete them before. 
* [GetInfo](#getinfo) - 
Return information about a specific key like its identifiers, its permissions and buckets on which it has permissions.
You can search by specifying the exact key identifier (`id`) or by specifying a pattern (`search`).

For confidentiality reasons, the secret key is not returned by default: you must pass the `showSecretKey` query parameter to get it.
    
* [Import](#import) - 
Imports an existing API key. This feature must only be used for migrations and backup restore.

**Do not use it to generate custom key identifiers or you will break your Garage cluster.**
    
* [List](#list) - Returns all API access keys in the cluster.
* [Update](#update) - 
Updates information about the specified API access key.

*Note: the secret key is not returned in the response, `null` is sent instead.*
    

## Create

Creates a new API access key.

### Example Usage

<!-- UsageSnippet language="go" operationID="CreateKey" method="post" path="/v2/CreateKey" -->
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

    res, err := s.AccessKeys.Create(ctx, components.CreateKeyRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.CreateKeyResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `ctx`                                                                      | [context.Context](https://pkg.go.dev/context#Context)                      | :heavy_check_mark:                                                         | The context to use for the request.                                        |
| `request`                                                                  | [components.CreateKeyRequest](../../models/components/createkeyrequest.md) | :heavy_check_mark:                                                         | The request object to use for the request.                                 |
| `opts`                                                                     | [][operations.Option](../../models/operations/option.md)                   | :heavy_minus_sign:                                                         | The options for this request.                                              |

### Response

**[*operations.CreateKeyResponse](../../models/operations/createkeyresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Delete

Delete a key from the cluster. Its access will be removed from all the buckets. Buckets are not automatically deleted and can be dangling. You should manually delete them before. 

### Example Usage

<!-- UsageSnippet language="go" operationID="DeleteKey" method="post" path="/v2/DeleteKey" -->
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

    res, err := s.AccessKeys.Delete(ctx, "<id>")
    if err != nil {
        log.Fatal(err)
    }
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | *string*                                                 | :heavy_check_mark:                                       | Access key ID                                            |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.DeleteKeyResponse](../../models/operations/deletekeyresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetInfo


Return information about a specific key like its identifiers, its permissions and buckets on which it has permissions.
You can search by specifying the exact key identifier (`id`) or by specifying a pattern (`search`).

For confidentiality reasons, the secret key is not returned by default: you must pass the `showSecretKey` query parameter to get it.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetKeyInfo" method="get" path="/v2/GetKeyInfo" -->
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

    res, err := s.AccessKeys.GetInfo(ctx, nil, nil, nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.CreateKeyResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | **string*                                                | :heavy_minus_sign:                                       | Access key ID                                            |
| `search`                                                 | **string*                                                | :heavy_minus_sign:                                       | Partial key ID or name to search for                     |
| `showSecretKey`                                          | **bool*                                                  | :heavy_minus_sign:                                       | Whether to return the secret access key                  |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.GetKeyInfoResponse](../../models/operations/getkeyinforesponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Import


Imports an existing API key. This feature must only be used for migrations and backup restore.

**Do not use it to generate custom key identifiers or you will break your Garage cluster.**
    

### Example Usage

<!-- UsageSnippet language="go" operationID="ImportKey" method="post" path="/v2/ImportKey" -->
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

    res, err := s.AccessKeys.Import(ctx, components.ImportKeyRequest{
        AccessKeyID: "<id>",
        SecretAccessKey: "<value>",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.CreateKeyResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `ctx`                                                                      | [context.Context](https://pkg.go.dev/context#Context)                      | :heavy_check_mark:                                                         | The context to use for the request.                                        |
| `request`                                                                  | [components.ImportKeyRequest](../../models/components/importkeyrequest.md) | :heavy_check_mark:                                                         | The request object to use for the request.                                 |
| `opts`                                                                     | [][operations.Option](../../models/operations/option.md)                   | :heavy_minus_sign:                                                         | The options for this request.                                              |

### Response

**[*operations.ImportKeyResponse](../../models/operations/importkeyresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## List

Returns all API access keys in the cluster.

### Example Usage

<!-- UsageSnippet language="go" operationID="ListKeys" method="get" path="/v2/ListKeys" -->
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

    res, err := s.AccessKeys.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListKeysResponse != nil {
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

**[*operations.ListKeysResponse](../../models/operations/listkeysresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Update


Updates information about the specified API access key.

*Note: the secret key is not returned in the response, `null` is sent instead.*
    

### Example Usage

<!-- UsageSnippet language="go" operationID="UpdateKey" method="post" path="/v2/UpdateKey" -->
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

    res, err := s.AccessKeys.Update(ctx, "<id>", components.CreateKeyRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.CreateKeyResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `ctx`                                                                      | [context.Context](https://pkg.go.dev/context#Context)                      | :heavy_check_mark:                                                         | The context to use for the request.                                        |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | Access key ID                                                              |
| `createKeyRequest`                                                         | [components.CreateKeyRequest](../../models/components/createkeyrequest.md) | :heavy_check_mark:                                                         | N/A                                                                        |
| `opts`                                                                     | [][operations.Option](../../models/operations/option.md)                   | :heavy_minus_sign:                                                         | The options for this request.                                              |

### Response

**[*operations.UpdateKeyResponse](../../models/operations/updatekeyresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |