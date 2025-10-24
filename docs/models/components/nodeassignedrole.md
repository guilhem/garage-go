# NodeAssignedRole


## Fields

| Field                                                                               | Type                                                                                | Required                                                                            | Description                                                                         |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `Capacity`                                                                          | **int64*                                                                            | :heavy_minus_sign:                                                                  | Capacity (in bytes) assigned by the cluster administrator,<br/>absent for gateway nodes |
| `Tags`                                                                              | []*string*                                                                          | :heavy_check_mark:                                                                  | List of tags assigned by the cluster administrator                                  |
| `Zone`                                                                              | *string*                                                                            | :heavy_check_mark:                                                                  | Zone name assigned by the cluster administrator                                     |