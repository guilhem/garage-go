# SpecialEndpoints
(*SpecialEndpoints*)

## Overview

### Available Operations

* [CheckDomain](#checkdomain) - 
Static website domain name check. Checks whether a bucket is configured to serve
a static website for the requested domain. This is used by reverse proxies such
as Caddy or Tricot, to avoid requesting TLS certificates for domain names that
do not correspond to an actual website.
    
* [Health](#health) - 
Check cluster health. The status code returned by this function indicates
whether this Garage daemon can answer API requests.
Garage will return `200 OK` even if some storage nodes are disconnected,
as long as it is able to have a quorum of nodes for read and write operations.
    
* [Metrics](#metrics) - Prometheus metrics endpoint

## CheckDomain


Static website domain name check. Checks whether a bucket is configured to serve
a static website for the requested domain. This is used by reverse proxies such
as Caddy or Tricot, to avoid requesting TLS certificates for domain names that
do not correspond to an actual website.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="CheckDomain" method="get" path="/check" -->
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

    res, err := s.SpecialEndpoints.CheckDomain(ctx, "outlandish-forager.org")
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
| `domain`                                                 | *string*                                                 | :heavy_check_mark:                                       | The domain name to check for                             |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.CheckDomainResponse](../../models/operations/checkdomainresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Health


Check cluster health. The status code returned by this function indicates
whether this Garage daemon can answer API requests.
Garage will return `200 OK` even if some storage nodes are disconnected,
as long as it is able to have a quorum of nodes for read and write operations.
    

### Example Usage

<!-- UsageSnippet language="go" operationID="Health" method="get" path="/health" -->
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

    res, err := s.SpecialEndpoints.Health(ctx)
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
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.HealthResponse](../../models/operations/healthresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Metrics

Prometheus metrics endpoint

### Example Usage

<!-- UsageSnippet language="go" operationID="Metrics" method="get" path="/metrics" -->
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

    res, err := s.SpecialEndpoints.Metrics(ctx, nil)
    if err != nil {
        log.Fatal(err)
    }
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `ctx`                                                                    | [context.Context](https://pkg.go.dev/context#Context)                    | :heavy_check_mark:                                                       | The context to use for the request.                                      |
| `security`                                                               | [operations.MetricsSecurity](../../models/operations/metricssecurity.md) | :heavy_check_mark:                                                       | The security requirements to use for the request.                        |
| `opts`                                                                   | [][operations.Option](../../models/operations/option.md)                 | :heavy_minus_sign:                                                       | The options for this request.                                            |

### Response

**[*operations.MetricsResponse](../../models/operations/metricsresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |