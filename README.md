# garage

Developer-friendly & type-safe Go SDK specifically catered to leverage *garage* API.

<div align="left" style="margin-bottom: 0;">
    <a href="https://www.speakeasy.com/?utm_source=garage&utm_campaign=go" class="badge-link">
        <span class="badge-container">
            <span class="badge-icon-section">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 30 30" fill="none" style="vertical-align: middle;"><title>Speakeasy Logo</title><path fill="currentColor" d="m20.639 27.548-19.17-2.724L0 26.1l20.639 2.931 8.456-7.336-1.468-.208-6.988 6.062Z"></path><path fill="currentColor" d="m20.639 23.1 8.456-7.336-1.468-.207-6.988 6.06-6.84-.972-9.394-1.333-2.936-.417L0 20.169l2.937.416L0 23.132l20.639 2.931 8.456-7.334-1.468-.208-6.986 6.062-9.78-1.39 1.468-1.273 8.31 1.18Z"></path><path fill="currentColor" d="m20.639 18.65-19.17-2.724L0 17.201l20.639 2.931 8.456-7.334-1.468-.208-6.988 6.06Z"></path><path fill="currentColor" d="M27.627 6.658 24.69 9.205 20.64 12.72l-7.923-1.126L1.469 9.996 0 11.271l11.246 1.596-1.467 1.275-8.311-1.181L0 14.235l20.639 2.932 8.456-7.334-2.937-.418 2.937-2.549-1.468-.208Z"></path><path fill="currentColor" d="M29.095 3.902 8.456.971 0 8.305l20.639 2.934 8.456-7.337Z"></path></svg>
            </span>
            <span class="badge-text badge-text-section">BUILT BY SPEAKEASY</span>
        </span>
    </a>
    <a href="https://opensource.org/licenses/MIT" class="badge-link">
        <span class="badge-container blue">
            <span class="badge-text badge-text-section">LICENSE // MIT</span>
        </span>
    </a>
</div>


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/barpilot/garage). Delete this section before > publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary

Garage administration API: Administrate your Garage cluster programatically, including status, layout, keys, buckets, and maintainance tasks.

*Disclaimer: This API may change in future Garage versions. Read the changelog and upgrade your scripts before upgrading. Additionnaly, this specification is early stage and can contain bugs, so be careful and please report any issues on our issue tracker.*
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [garage](#garage)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

To add the SDK as a dependency to your project:
```bash
go get github.com/guilhem/garage-go
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```go
package main

import (
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
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name         | Type | Scheme      | Environment Variable |
| ------------ | ---- | ----------- | -------------------- |
| `BearerAuth` | http | HTTP Bearer | `GARAGE_BEARER_AUTH` |

You can configure it using the `WithSecurity` option when initializing the SDK client instance. For example:
```go
package main

import (
	"context"
	garage "github.com/guilhem/garage-go"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := garage.New(
		garage.WithSecurity(os.Getenv("GARAGE_BEARER_AUTH")),
	)

	res, err := s.SpecialEndpoints.CheckDomain(ctx, "outlandish-forager.org")
	if err != nil {
		log.Fatal(err)
	}
	if res != nil {
		// handle response
	}
}

```

### Per-Operation Security Schemes

Some operations in this SDK require the security scheme to be specified at the request level. For example:
```go
package main

import (
	"context"
	garage "github.com/guilhem/garage-go"
	"github.com/guilhem/garage-go/models/operations"
	"log"
)

func main() {
	ctx := context.Background()

	s := garage.New()

	res, err := s.SpecialEndpoints.Metrics(ctx, garage.Pointer(operations.MetricsSecurity{}))
	if err != nil {
		log.Fatal(err)
	}
	if res != nil {
		// handle response
	}
}

```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [AccessKeys](docs/sdks/accesskeys/README.md)

* [Create](docs/sdks/accesskeys/README.md#create) - Creates a new API access key.
* [Delete](docs/sdks/accesskeys/README.md#delete) - Delete a key from the cluster. Its access will be removed from all the buckets. Buckets are not automatically deleted and can be dangling. You should manually delete them before. 
* [GetInfo](docs/sdks/accesskeys/README.md#getinfo) - 
Return information about a specific key like its identifiers, its permissions and buckets on which it has permissions.
You can search by specifying the exact key identifier (`id`) or by specifying a pattern (`search`).

For confidentiality reasons, the secret key is not returned by default: you must pass the `showSecretKey` query parameter to get it.
    
* [Import](docs/sdks/accesskeys/README.md#import) - 
Imports an existing API key. This feature must only be used for migrations and backup restore.

**Do not use it to generate custom key identifiers or you will break your Garage cluster.**
    
* [List](docs/sdks/accesskeys/README.md#list) - Returns all API access keys in the cluster.
* [Update](docs/sdks/accesskeys/README.md#update) - 
Updates information about the specified API access key.

*Note: the secret key is not returned in the response, `null` is sent instead.*
    

### [AdminAPITokens](docs/sdks/adminapitokens/README.md)

* [Create](docs/sdks/adminapitokens/README.md#create) - Creates a new admin API token
* [Delete](docs/sdks/adminapitokens/README.md#delete) - Delete an admin API token from the cluster, revoking all its permissions.
* [GetInfo](docs/sdks/adminapitokens/README.md#getinfo) - 
Return information about a specific admin API token.
You can search by specifying the exact token identifier (`id`) or by specifying a pattern (`search`).
    
* [GetCurrentInfo](docs/sdks/adminapitokens/README.md#getcurrentinfo) - 
Return information about the calling admin API token.
    
* [List](docs/sdks/adminapitokens/README.md#list) - Returns all admin API tokens in the cluster.
* [Update](docs/sdks/adminapitokens/README.md#update) - 
Updates information about the specified admin API token.
    

### [Blocks](docs/sdks/blocks/README.md)

* [GetInfo](docs/sdks/blocks/README.md#getinfo) - 
Get detailed information about a data block stored on a Garage node, including all object versions and in-progress multipart uploads that contain a reference to this block.
    
* [ListErrors](docs/sdks/blocks/README.md#listerrors) - 
List data blocks that are currently in an errored state on one or several Garage nodes.
    
* [Purge](docs/sdks/blocks/README.md#purge) - 
Purge references to one or several missing data blocks.

This will remove all objects and in-progress multipart uploads that contain the specified data block(s). The objects will be permanently deleted from the buckets in which they appear. Use with caution.
    
* [RetryResync](docs/sdks/blocks/README.md#retryresync) - 
Instruct Garage node(s) to retry the resynchronization of one or several missing data block(s).
    

### [Bucket](docs/sdks/bucket/README.md)

* [GetInfo](docs/sdks/bucket/README.md#getinfo) - 
Given a bucket identifier (`id`) or a global alias (`alias`), get its information.
It includes its aliases, its web configuration, keys that have some permissions
on it, some statistics (number of objects, size), number of dangling multipart uploads,
and its quotas (if any).
    

### [BucketAliases](docs/sdks/bucketaliases/README.md)

* [Add](docs/sdks/bucketaliases/README.md#add) - Add an alias for the target bucket.  This can be either a global or a local alias, depending on which fields are specified.
* [Remove](docs/sdks/bucketaliases/README.md#remove) - Remove an alias for the target bucket.  This can be either a global or a local alias, depending on which fields are specified.

### [Buckets](docs/sdks/buckets/README.md)

* [CleanupIncompleteUploads](docs/sdks/buckets/README.md#cleanupincompleteuploads) - Removes all incomplete multipart uploads that are older than the specified number of seconds.
* [Create](docs/sdks/buckets/README.md#create) - 
Creates a new bucket, either with a global alias, a local one, or no alias at all.
Technically, you can also specify both `globalAlias` and `localAlias` and that would create two aliases.
    
* [Delete](docs/sdks/buckets/README.md#delete) - 
Deletes a storage bucket. A bucket cannot be deleted if it is not empty.

**Warning:** this will delete all aliases associated with the bucket!
    
* [InspectObject](docs/sdks/buckets/README.md#inspectobject) - 
Returns detailed information about an object in a bucket, including its internal state in Garage.

This API call can be used to list the data blocks referenced by an object,
as well as to view metadata associated to the object.

This call may return a list of more than one version for the object, for instance in the
case where there is a currently stored version of the object, and a newer version whose
upload is in progress and not yet finished.
    
* [List](docs/sdks/buckets/README.md#list) - List all the buckets on the cluster with their UUID and their global and local aliases.
* [Update](docs/sdks/buckets/README.md#update) - 
All fields (`websiteAccess` and `quotas`) are optional.
If they are present, the corresponding modifications are applied to the bucket, otherwise nothing is changed.

In `websiteAccess`: if `enabled` is `true`, `indexDocument` must be specified.
The field `errorDocument` is optional, if no error document is set a generic
error message is displayed when errors happen. Conversely, if `enabled` is
`false`, neither `indexDocument` nor `errorDocument` must be specified.

In `quotas`: new values of `maxSize` and `maxObjects` must both be specified, or set to `null`
to remove the quotas. An absent value will be considered the same as a `null`. It is not possible
to change only one of the two quotas.
    

### [Cluster](docs/sdks/cluster/README.md)

* [GetHealth](docs/sdks/cluster/README.md#gethealth) - Returns the global status of the cluster, the number of connected nodes (over the number of known ones), the number of healthy storage nodes (over the declared ones), and the number of healthy partitions (over the total).
* [GetStatus](docs/sdks/cluster/README.md#getstatus) - 
Returns the cluster's current status, including:

- ID of the node being queried and its version of the Garage daemon
- Live nodes
- Currently configured cluster layout
- Staged changes to the cluster layout

*Capacity is given in bytes*
    

### [ClusterLayout](docs/sdks/clusterlayout/README.md)

* [Apply](docs/sdks/clusterlayout/README.md#apply) - 
Applies to the cluster the layout changes currently registered as staged layout changes.

*Note: do not try to parse the `message` field of the response, it is given as an array of string specifically because its format is not stable.*
    
* [SkipDeadNodes](docs/sdks/clusterlayout/README.md#skipdeadnodes) - Force progress in layout update trackers
* [Get](docs/sdks/clusterlayout/README.md#get) - 
Returns the cluster's current layout, including:

- Currently configured cluster layout
- Staged changes to the cluster layout

*Capacity is given in bytes*
    
* [GetHistory](docs/sdks/clusterlayout/README.md#gethistory) - 
Returns the history of layouts in the cluster
    
* [PreviewChanges](docs/sdks/clusterlayout/README.md#previewchanges) - 
Computes a new layout taking into account the staged parameters, and returns it with detailed statistics. The new layout is not applied in the cluster.

*Note: do not try to parse the `message` field of the response, it is given as an array of string specifically because its format is not stable.*
    
* [Revert](docs/sdks/clusterlayout/README.md#revert) - Clear staged layout changes
* [Update](docs/sdks/clusterlayout/README.md#update) - 
Send modifications to the cluster layout. These modifications will be included in the staged role changes, visible in subsequent calls of `GET /GetClusterHealth`. Once the set of staged changes is satisfactory, the user may call `POST /ApplyClusterLayout` to apply the changed changes, or `POST /RevertClusterLayout` to clear all of the staged changes in the layout.

Setting the capacity to `null` will configure the node as a gateway.
Otherwise, capacity must be now set in bytes (before Garage 0.9 it was arbitrary weights).
For example to declare 100GB, you must set `capacity: 100000000000`.

Garage uses internally the International System of Units (SI), it assumes that 1kB = 1000 bytes, and displays storage as kB, MB, GB (and not KiB, MiB, GiB that assume 1KiB = 1024 bytes).
    

### [Clusters](docs/sdks/clusters/README.md)

* [ConnectNodes](docs/sdks/clusters/README.md#connectnodes) - Instructs this Garage node to connect to other Garage nodes at specified `<node_id>@<net_address>`. `node_id` is generated automatically on node start.
* [GetStatistics](docs/sdks/clusters/README.md#getstatistics) - 
Fetch global cluster statistics.

*Note: do not try to parse the `freeform` field of the response, it is given as a string specifically because its format is not stable.*
    

### [Nodes](docs/sdks/nodes/README.md)

* [CreateMetadataSnapshot](docs/sdks/nodes/README.md#createmetadatasnapshot) - 
Instruct one or several nodes to take a snapshot of their metadata databases.
    
* [GetInfo](docs/sdks/nodes/README.md#getinfo) - 
Return information about the Garage daemon running on one or several nodes.
    
* [GetStatistics](docs/sdks/nodes/README.md#getstatistics) - 
Fetch statistics for one or several Garage nodes.

*Note: do not try to parse the `freeform` field of the response, it is given as a string specifically because its format is not stable.*
    
* [LaunchRepairOperation](docs/sdks/nodes/README.md#launchrepairoperation) - 
Launch a repair operation on one or several cluster nodes.
    

### [Permissions](docs/sdks/permissions/README.md)

* [AllowBucketKey](docs/sdks/permissions/README.md#allowbucketkey) - 
⚠️ **DISCLAIMER**: Garage's developers are aware that this endpoint has an unconventional semantic. Be extra careful when implementing it, its behavior is not obvious.

Allows a key to do read/write/owner operations on a bucket.

Flags in permissions which have the value true will be activated. Other flags will remain unchanged (ie. they will keep their internal value).

For example, if you set read to true, the key will be allowed to read the bucket.
If you set it to false, the key will keeps its previous read permission.
If you want to disallow read for the key, check the DenyBucketKey operation.
    
* [DenyBucketKey](docs/sdks/permissions/README.md#denybucketkey) - 
⚠️ **DISCLAIMER**: Garage's developers are aware that this endpoint has an unconventional semantic. Be extra careful when implementing it, its behavior is not obvious.

Denies a key from doing read/write/owner operations on a bucket.

Flags in permissions which have the value true will be deactivated. Other flags will remain unchanged.

For example, if you set read to true, the key will be denied from reading.
If you set read to false,  the key will keep its previous permissions.
If you want the key to have the reading permission, check the AllowBucketKey operation.
    

### [SpecialEndpoints](docs/sdks/specialendpoints/README.md)

* [CheckDomain](docs/sdks/specialendpoints/README.md#checkdomain) - 
Static website domain name check. Checks whether a bucket is configured to serve
a static website for the requested domain. This is used by reverse proxies such
as Caddy or Tricot, to avoid requesting TLS certificates for domain names that
do not correspond to an actual website.
    
* [Health](docs/sdks/specialendpoints/README.md#health) - 
Check cluster health. The status code returned by this function indicates
whether this Garage daemon can answer API requests.
Garage will return `200 OK` even if some storage nodes are disconnected,
as long as it is able to have a quorum of nodes for read and write operations.
    
* [Metrics](docs/sdks/specialendpoints/README.md#metrics) - Prometheus metrics endpoint

### [Workers](docs/sdks/workers/README.md)

* [GetInfo](docs/sdks/workers/README.md#getinfo) - 
Get information about the specified background worker on one or several cluster nodes.
    
* [GetVariable](docs/sdks/workers/README.md#getvariable) - 
Fetch values of one or several worker variables, from one or several cluster nodes.
    
* [List](docs/sdks/workers/README.md#list) - 
List background workers currently running on one or several cluster nodes.
    
* [SetVariable](docs/sdks/workers/README.md#setvariable) - 
Set the value for a worker variable, on one or several cluster nodes.
    

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `retry.Config` object to the call by using the `WithRetries` option:
```go
package main

import (
	"context"
	garage "github.com/guilhem/garage-go"
	"github.com/guilhem/garage-go/retry"
	"log"
	"models/operations"
)

func main() {
	ctx := context.Background()

	s := garage.New()

	res, err := s.SpecialEndpoints.CheckDomain(ctx, "outlandish-forager.org", operations.WithRetries(
		retry.Config{
			Strategy: "backoff",
			Backoff: &retry.BackoffStrategy{
				InitialInterval: 1,
				MaxInterval:     50,
				Exponent:        1.1,
				MaxElapsedTime:  100,
			},
			RetryConnectionErrors: false,
		}))
	if err != nil {
		log.Fatal(err)
	}
	if res != nil {
		// handle response
	}
}

```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `WithRetryConfig` option at SDK initialization:
```go
package main

import (
	"context"
	garage "github.com/guilhem/garage-go"
	"github.com/guilhem/garage-go/retry"
	"log"
)

func main() {
	ctx := context.Background()

	s := garage.New(
		garage.WithRetryConfig(
			retry.Config{
				Strategy: "backoff",
				Backoff: &retry.BackoffStrategy{
					InitialInterval: 1,
					MaxInterval:     50,
					Exponent:        1.1,
					MaxElapsedTime:  100,
				},
				RetryConnectionErrors: false,
			}),
	)

	res, err := s.SpecialEndpoints.CheckDomain(ctx, "outlandish-forager.org")
	if err != nil {
		log.Fatal(err)
	}
	if res != nil {
		// handle response
	}
}

```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or an error, they will never return both.

By Default, an API error will return `apierrors.APIError`. When custom error responses are specified for an operation, the SDK may also return their associated error. You can refer to respective *Errors* tables in SDK docs for more details on possible error types for each operation.

For example, the `CheckDomain` function may return the following errors:

| Error Type         | Status Code | Content Type |
| ------------------ | ----------- | ------------ |
| apierrors.APIError | 4XX, 5XX    | \*/\*        |

### Example

```go
package main

import (
	"context"
	"errors"
	garage "github.com/guilhem/garage-go"
	"github.com/guilhem/garage-go/models/apierrors"
	"log"
)

func main() {
	ctx := context.Background()

	s := garage.New()

	res, err := s.SpecialEndpoints.CheckDomain(ctx, "outlandish-forager.org")
	if err != nil {

		var e *apierrors.APIError
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}
	}
}

```
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Override Server URL Per-Client

The default server can be overridden globally using the `WithServerURL(serverURL string)` option when initializing the SDK client instance. For example:
```go
package main

import (
	"context"
	garage "github.com/guilhem/garage-go"
	"log"
)

func main() {
	ctx := context.Background()

	s := garage.New(
		garage.WithServerURL("http://localhost:3903/"),
	)

	res, err := s.SpecialEndpoints.CheckDomain(ctx, "outlandish-forager.org")
	if err != nil {
		log.Fatal(err)
	}
	if res != nil {
		// handle response
	}
}

```
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Go SDK makes API calls that wrap an internal HTTP client. The requirements for the HTTP client are very simple. It must match this interface:

```go
type HTTPClient interface {
	Do(req *http.Request) (*http.Response, error)
}
```

The built-in `net/http` client satisfies this interface and a default client based on the built-in is provided by default. To replace this default with a client of your own, you can implement this interface yourself or provide your own client configured as desired. Here's a simple example, which adds a client with a 30 second timeout.

```go
import (
	"net/http"
	"time"

	"github.com/guilhem/garage-go"
)

var (
	httpClient = &http.Client{Timeout: 30 * time.Second}
	sdkClient  = garage.New(garage.WithClient(httpClient))
)
```

This can be a convenient way to configure timeouts, cookies, proxies, custom headers, and other low-level configuration.
<!-- End Custom HTTP Client [http-client] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=garage&utm_campaign=go)

<style>
  :root {
    --badge-gray-bg: #f3f4f6;
    --badge-gray-border: #d1d5db;
    --badge-gray-text: #374151;
    --badge-blue-bg: #eff6ff;
    --badge-blue-border: #3b82f6;
    --badge-blue-text: #3b82f6;
  }

  @media (prefers-color-scheme: dark) {
    :root {
      --badge-gray-bg: #374151;
      --badge-gray-border: #4b5563;
      --badge-gray-text: #f3f4f6;
      --badge-blue-bg: #1e3a8a;
      --badge-blue-border: #3b82f6;
      --badge-blue-text: #93c5fd;
    }
  }
  
  h1 {
    border-bottom: none !important;
    margin-bottom: 4px;
    margin-top: 0;
    letter-spacing: 0.5px;
    font-weight: 600;
  }
  
  .badge-text {
    letter-spacing: 1px;
    font-weight: 300;
  }
  
  .badge-container {
    display: inline-flex;
    align-items: center;
    background: var(--badge-gray-bg);
    border: 1px solid var(--badge-gray-border);
    border-radius: 6px;
    overflow: hidden;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
    font-size: 11px;
    text-decoration: none;
    vertical-align: middle;
  }

  .badge-container.blue {
    background: var(--badge-blue-bg);
    border-color: var(--badge-blue-border);
  }

  .badge-icon-section {
    padding: 4px 8px;
    border-right: 1px solid var(--badge-gray-border);
    display: flex;
    align-items: center;
  }

  .badge-text-section {
    padding: 4px 10px;
    color: var(--badge-gray-text);
    font-weight: 400;
  }

  .badge-container.blue .badge-text-section {
    color: var(--badge-blue-text);
  }
  
  .badge-link {
    text-decoration: none;
    margin-left: 8px;
    display: inline-flex;
    vertical-align: middle;
  }

  .badge-link:hover {
    text-decoration: none;
  }
  
  .badge-link:first-child {
    margin-left: 0;
  }
  
  .badge-icon-section svg {
    color: var(--badge-gray-text);
  }

  .badge-container.blue .badge-icon-section svg {
    color: var(--badge-blue-text);
  }
</style> 