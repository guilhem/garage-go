# ConnectNodeResponse


## Fields

| Field                                                             | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `Error`                                                           | **string*                                                         | :heavy_minus_sign:                                                | An error message if Garage did not manage to connect to this node |
| `Success`                                                         | *bool*                                                            | :heavy_check_mark:                                                | `true` if Garage managed to connect to this node                  |