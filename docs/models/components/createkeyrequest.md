# CreateKeyRequest


## Fields

| Field                                                     | Type                                                      | Required                                                  | Description                                               |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| `Allow`                                                   | [*components.KeyPerm](../../models/components/keyperm.md) | :heavy_minus_sign:                                        | N/A                                                       |
| `Deny`                                                    | [*components.KeyPerm](../../models/components/keyperm.md) | :heavy_minus_sign:                                        | N/A                                                       |
| `Expiration`                                              | [*time.Time](https://pkg.go.dev/time#Time)                | :heavy_minus_sign:                                        | Expiration time and date, formatted according to RFC 3339 |
| `Name`                                                    | **string*                                                 | :heavy_minus_sign:                                        | Name of the API key                                       |
| `NeverExpires`                                            | **bool*                                                   | :heavy_minus_sign:                                        | Set the access key to never expire                        |