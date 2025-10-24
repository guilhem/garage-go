# InspectObjectBlock


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `Hash`                                                               | *string*                                                             | :heavy_check_mark:                                                   | Hash (blake2 sum) of the block's data                                |
| `Offset`                                                             | *int64*                                                              | :heavy_check_mark:                                                   | Offset of this block within the part                                 |
| `PartNumber`                                                         | *int64*                                                              | :heavy_check_mark:                                                   | Part number of the part containing this block, for multipart uploads |
| `Size`                                                               | *int64*                                                              | :heavy_check_mark:                                                   | Length of the blocks's data                                          |