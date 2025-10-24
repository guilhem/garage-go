# Workers
(*Workers*)

## Overview

### Available Operations

* [GetInfo](#getinfo) - 
Get information about the specified background worker on one or several cluster nodes.
    
* [GetVariable](#getvariable) - 
Fetch values of one or several worker variables, from one or several cluster nodes.
    
* [List](#list) - 
List background workers currently running on one or several cluster nodes.
    
* [SetVariable](#setvariable) - 
Set the value for a worker variable, on one or several cluster nodes.
    

## GetInfo


Get information about the specified background worker on one or several cluster nodes.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetWorkerInfo" method="post" path="/v2/GetWorkerInfo" -->
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

    res, err := s.Workers.GetInfo(ctx, "<value>", components.LocalGetWorkerInfoRequest{
        ID: 847670,
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalGetWorkerInfoResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                    | Type                                                                                         | Required                                                                                     | Description                                                                                  |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `ctx`                                                                                        | [context.Context](https://pkg.go.dev/context#Context)                                        | :heavy_check_mark:                                                                           | The context to use for the request.                                                          |
| `node`                                                                                       | *string*                                                                                     | :heavy_check_mark:                                                                           | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request     |
| `localGetWorkerInfoRequest`                                                                  | [components.LocalGetWorkerInfoRequest](../../models/components/localgetworkerinforequest.md) | :heavy_check_mark:                                                                           | N/A                                                                                          |
| `opts`                                                                                       | [][operations.Option](../../models/operations/option.md)                                     | :heavy_minus_sign:                                                                           | The options for this request.                                                                |

### Response

**[*operations.GetWorkerInfoResponse](../../models/operations/getworkerinforesponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## GetVariable


Fetch values of one or several worker variables, from one or several cluster nodes.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="GetWorkerVariable" method="post" path="/v2/GetWorkerVariable" -->
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

    res, err := s.Workers.GetVariable(ctx, "<value>", components.LocalGetWorkerVariableRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalGetWorkerVariableResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                                | :heavy_check_mark:                                                                                   | The context to use for the request.                                                                  |
| `node`                                                                                               | *string*                                                                                             | :heavy_check_mark:                                                                                   | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request             |
| `localGetWorkerVariableRequest`                                                                      | [components.LocalGetWorkerVariableRequest](../../models/components/localgetworkervariablerequest.md) | :heavy_check_mark:                                                                                   | N/A                                                                                                  |
| `opts`                                                                                               | [][operations.Option](../../models/operations/option.md)                                             | :heavy_minus_sign:                                                                                   | The options for this request.                                                                        |

### Response

**[*operations.GetWorkerVariableResponse](../../models/operations/getworkervariableresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## List


List background workers currently running on one or several cluster nodes.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="ListWorkers" method="post" path="/v2/ListWorkers" -->
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

    res, err := s.Workers.List(ctx, "<value>", components.LocalListWorkersRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalListWorkersResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |
| `node`                                                                                   | *string*                                                                                 | :heavy_check_mark:                                                                       | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request |
| `localListWorkersRequest`                                                                | [components.LocalListWorkersRequest](../../models/components/locallistworkersrequest.md) | :heavy_check_mark:                                                                       | N/A                                                                                      |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |

### Response

**[*operations.ListWorkersResponse](../../models/operations/listworkersresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## SetVariable


Set the value for a worker variable, on one or several cluster nodes.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="SetWorkerVariable" method="post" path="/v2/SetWorkerVariable" -->
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

    res, err := s.Workers.SetVariable(ctx, "<value>", components.LocalSetWorkerVariableRequest{
        Value: "<value>",
        Variable: "<value>",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.MultiResponseLocalSetWorkerVariableResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                                | :heavy_check_mark:                                                                                   | The context to use for the request.                                                                  |
| `node`                                                                                               | *string*                                                                                             | :heavy_check_mark:                                                                                   | Node ID to query, or `*` for all nodes, or `self` for the node responding to the request             |
| `localSetWorkerVariableRequest`                                                                      | [components.LocalSetWorkerVariableRequest](../../models/components/localsetworkervariablerequest.md) | :heavy_check_mark:                                                                                   | N/A                                                                                                  |
| `opts`                                                                                               | [][operations.Option](../../models/operations/option.md)                                             | :heavy_minus_sign:                                                                                   | The options for this request.                                                                        |

### Response

**[*operations.SetWorkerVariableResponse](../../models/operations/setworkervariableresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |