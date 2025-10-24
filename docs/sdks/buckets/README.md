# Buckets
(*Buckets*)

## Overview

### Available Operations

* [CleanupIncompleteUploads](#cleanupincompleteuploads) - Removes all incomplete multipart uploads that are older than the specified number of seconds.
* [Create](#create) - 
Creates a new bucket, either with a global alias, a local one, or no alias at all.
Technically, you can also specify both `globalAlias` and `localAlias` and that would create two aliases.
    
* [Delete](#delete) - 
Deletes a storage bucket. A bucket cannot be deleted if it is not empty.

**Warning:** this will delete all aliases associated with the bucket!
    
* [InspectObject](#inspectobject) - 
Returns detailed information about an object in a bucket, including its internal state in Garage.

This API call can be used to list the data blocks referenced by an object,
as well as to view metadata associated to the object.

This call may return a list of more than one version for the object, for instance in the
case where there is a currently stored version of the object, and a newer version whose
upload is in progress and not yet finished.
    
* [List](#list) - List all the buckets on the cluster with their UUID and their global and local aliases.
* [Update](#update) - 
All fields (`websiteAccess` and `quotas`) are optional.
If they are present, the corresponding modifications are applied to the bucket, otherwise nothing is changed.

In `websiteAccess`: if `enabled` is `true`, `indexDocument` must be specified.
The field `errorDocument` is optional, if no error document is set a generic
error message is displayed when errors happen. Conversely, if `enabled` is
`false`, neither `indexDocument` nor `errorDocument` must be specified.

In `quotas`: new values of `maxSize` and `maxObjects` must both be specified, or set to `null`
to remove the quotas. An absent value will be considered the same as a `null`. It is not possible
to change only one of the two quotas.
    

## CleanupIncompleteUploads

Removes all incomplete multipart uploads that are older than the specified number of seconds.

### Example Usage

<!-- UsageSnippet language="go" operationID="CleanupIncompleteUploads" method="post" path="/v2/CleanupIncompleteUploads" -->
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

    res, err := s.Buckets.CleanupIncompleteUploads(ctx, components.CleanupIncompleteUploadsRequest{
        BucketID: "<id>",
        OlderThanSecs: 663838,
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.CleanupIncompleteUploadsResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                | Type                                                                                                     | Required                                                                                                 | Description                                                                                              |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                                    | :heavy_check_mark:                                                                                       | The context to use for the request.                                                                      |
| `request`                                                                                                | [components.CleanupIncompleteUploadsRequest](../../models/components/cleanupincompleteuploadsrequest.md) | :heavy_check_mark:                                                                                       | The request object to use for the request.                                                               |
| `opts`                                                                                                   | [][operations.Option](../../models/operations/option.md)                                                 | :heavy_minus_sign:                                                                                       | The options for this request.                                                                            |

### Response

**[*operations.CleanupIncompleteUploadsResponse](../../models/operations/cleanupincompleteuploadsresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Create


Creates a new bucket, either with a global alias, a local one, or no alias at all.
Technically, you can also specify both `globalAlias` and `localAlias` and that would create two aliases.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="CreateBucket" method="post" path="/v2/CreateBucket" -->
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

    res, err := s.Buckets.Create(ctx, components.CreateBucketRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.AddBucketAliasResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [components.CreateBucketRequest](../../models/components/createbucketrequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.CreateBucketResponse](../../models/operations/createbucketresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Delete


Deletes a storage bucket. A bucket cannot be deleted if it is not empty.

**Warning:** this will delete all aliases associated with the bucket!
    

### Example Usage

<!-- UsageSnippet language="go" operationID="DeleteBucket" method="post" path="/v2/DeleteBucket" -->
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

    res, err := s.Buckets.Delete(ctx, "<id>")
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
| `id`                                                     | *string*                                                 | :heavy_check_mark:                                       | ID of the bucket to delete                               |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.DeleteBucketResponse](../../models/operations/deletebucketresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## InspectObject


Returns detailed information about an object in a bucket, including its internal state in Garage.

This API call can be used to list the data blocks referenced by an object,
as well as to view metadata associated to the object.

This call may return a list of more than one version for the object, for instance in the
case where there is a currently stored version of the object, and a newer version whose
upload is in progress and not yet finished.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="InspectObject" method="get" path="/v2/InspectObject" -->
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

    res, err := s.Buckets.InspectObject(ctx, "<id>", "<key>")
    if err != nil {
        log.Fatal(err)
    }
    if res.InspectObjectResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `bucketID`                                               | *string*                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `key`                                                    | *string*                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.InspectObjectResponse](../../models/operations/inspectobjectresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## List

List all the buckets on the cluster with their UUID and their global and local aliases.

### Example Usage

<!-- UsageSnippet language="go" operationID="ListBuckets" method="get" path="/v2/ListBuckets" -->
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

    res, err := s.Buckets.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListBucketsResponse != nil {
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

**[*operations.ListBucketsResponse](../../models/operations/listbucketsresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Update


All fields (`websiteAccess` and `quotas`) are optional.
If they are present, the corresponding modifications are applied to the bucket, otherwise nothing is changed.

In `websiteAccess`: if `enabled` is `true`, `indexDocument` must be specified.
The field `errorDocument` is optional, if no error document is set a generic
error message is displayed when errors happen. Conversely, if `enabled` is
`false`, neither `indexDocument` nor `errorDocument` must be specified.

In `quotas`: new values of `maxSize` and `maxObjects` must both be specified, or set to `null`
to remove the quotas. An absent value will be considered the same as a `null`. It is not possible
to change only one of the two quotas.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="UpdateBucket" method="post" path="/v2/UpdateBucket" -->
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

    res, err := s.Buckets.Update(ctx, "<id>", components.UpdateBucketRequestBody{})
    if err != nil {
        log.Fatal(err)
    }
    if res.AddBucketAliasResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |
| `id`                                                                                     | *string*                                                                                 | :heavy_check_mark:                                                                       | ID of the bucket to update                                                               |
| `updateBucketRequestBody`                                                                | [components.UpdateBucketRequestBody](../../models/components/updatebucketrequestbody.md) | :heavy_check_mark:                                                                       | N/A                                                                                      |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |

### Response

**[*operations.UpdateBucketResponse](../../models/operations/updatebucketresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |