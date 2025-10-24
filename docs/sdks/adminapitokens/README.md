# AdminAPITokens
(*AdminAPITokens*)

## Overview

### Available Operations

* [Create](#create) - Creates a new admin API token
* [Delete](#delete) - Delete an admin API token from the cluster, revoking all its permissions.
* [GetInfo](#getinfo) - 
Return information about a specific admin API token.
You can search by specifying the exact token identifier (`id`) or by specifying a pattern (`search`).
    
* [GetCurrentInfo](#getcurrentinfo) - 
Return information about the calling admin API token.
    
* [List](#list) - Returns all admin API tokens in the cluster.
* [Update](#update) - 
Updates information about the specified admin API token.
    

## Create

Creates a new admin API token

### Example Usage

<!-- UsageSnippet language="go" operationID="CreateAdminToken" method="post" path="/v2/CreateAdminToken" -->
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

    res, err := s.AdminAPITokens.Create(ctx, components.UpdateAdminTokenRequestBody{})
    if err != nil {
        log.Fatal(err)
    }
    if res.CreateAdminTokenResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                        | Type                                                                                             | Required                                                                                         | Description                                                                                      |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                            | [context.Context](https://pkg.go.dev/context#Context)                                            | :heavy_check_mark:                                                                               | The context to use for the request.                                                              |
| `request`                                                                                        | [components.UpdateAdminTokenRequestBody](../../models/components/updateadmintokenrequestbody.md) | :heavy_check_mark:                                                                               | The request object to use for the request.                                                       |
| `opts`                                                                                           | [][operations.Option](../../models/operations/option.md)                                         | :heavy_minus_sign:                                                                               | The options for this request.                                                                    |

### Response

**[*operations.CreateAdminTokenResponse](../../models/operations/createadmintokenresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Delete

Delete an admin API token from the cluster, revoking all its permissions.

### Example Usage

<!-- UsageSnippet language="go" operationID="DeleteAdminToken" method="post" path="/v2/DeleteAdminToken" -->
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

    res, err := s.AdminAPITokens.Delete(ctx, "<id>")
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
| `id`                                                     | *string*                                                 | :heavy_check_mark:                                       | Admin API token ID                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.DeleteAdminTokenResponse](../../models/operations/deleteadmintokenresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetInfo


Return information about a specific admin API token.
You can search by specifying the exact token identifier (`id`) or by specifying a pattern (`search`).
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetAdminTokenInfo" method="get" path="/v2/GetAdminTokenInfo" -->
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

    res, err := s.AdminAPITokens.GetInfo(ctx, nil, nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetAdminTokenInfoResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | **string*                                                | :heavy_minus_sign:                                       | Admin API token ID                                       |
| `search`                                                 | **string*                                                | :heavy_minus_sign:                                       | Partial token ID or name to search for                   |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.GetAdminTokenInfoResponse](../../models/operations/getadmintokeninforesponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetCurrentInfo


Return information about the calling admin API token.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetCurrentAdminTokenInfo" method="get" path="/v2/GetCurrentAdminTokenInfo" -->
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

    res, err := s.AdminAPITokens.GetCurrentInfo(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GetAdminTokenInfoResponse != nil {
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

**[*operations.GetCurrentAdminTokenInfoResponse](../../models/operations/getcurrentadmintokeninforesponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## List

Returns all admin API tokens in the cluster.

### Example Usage

<!-- UsageSnippet language="go" operationID="ListAdminTokens" method="get" path="/v2/ListAdminTokens" -->
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

    res, err := s.AdminAPITokens.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListAdminTokensResponse != nil {
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

**[*operations.ListAdminTokensResponse](../../models/operations/listadmintokensresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Update


Updates information about the specified admin API token.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="UpdateAdminToken" method="post" path="/v2/UpdateAdminToken" -->
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

    res, err := s.AdminAPITokens.Update(ctx, "<id>", components.UpdateAdminTokenRequestBody{})
    if err != nil {
        log.Fatal(err)
    }
    if res.GetAdminTokenInfoResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                        | Type                                                                                             | Required                                                                                         | Description                                                                                      |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                            | [context.Context](https://pkg.go.dev/context#Context)                                            | :heavy_check_mark:                                                                               | The context to use for the request.                                                              |
| `id`                                                                                             | *string*                                                                                         | :heavy_check_mark:                                                                               | Admin API token ID                                                                               |
| `updateAdminTokenRequestBody`                                                                    | [components.UpdateAdminTokenRequestBody](../../models/components/updateadmintokenrequestbody.md) | :heavy_check_mark:                                                                               | N/A                                                                                              |
| `opts`                                                                                           | [][operations.Option](../../models/operations/option.md)                                         | :heavy_minus_sign:                                                                               | The options for this request.                                                                    |

### Response

**[*operations.UpdateAdminTokenResponse](../../models/operations/updateadmintokenresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |