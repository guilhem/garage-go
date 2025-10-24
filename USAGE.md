<!-- Start SDK Example Usage [usage] -->
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