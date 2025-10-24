# Bucket
(*Bucket*)

## Overview

### Available Operations

* [GetInfo](#getinfo) - 
Given a bucket identifier (`id`) or a global alias (`alias`), get its information.
It includes its aliases, its web configuration, keys that have some permissions
on it, some statistics (number of objects, size), number of dangling multipart uploads,
and its quotas (if any).
    

## GetInfo


Given a bucket identifier (`id`) or a global alias (`alias`), get its information.
It includes its aliases, its web configuration, keys that have some permissions
on it, some statistics (number of objects, size), number of dangling multipart uploads,
and its quotas (if any).
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetBucketInfo" method="get" path="/v2/GetBucketInfo" -->
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

    res, err := s.Bucket.GetInfo(ctx, nil, nil, nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.AddBucketAliasResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | **string*                                                | :heavy_minus_sign:                                       | Exact bucket ID to look up                               |
| `globalAlias`                                            | **string*                                                | :heavy_minus_sign:                                       | Global alias of bucket to look up                        |
| `search`                                                 | **string*                                                | :heavy_minus_sign:                                       | Partial ID or alias to search for                        |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.GetBucketInfoResponse](../../models/operations/getbucketinforesponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |