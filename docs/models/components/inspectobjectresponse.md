# InspectObjectResponse


## Fields

| Field                                                                                | Type                                                                                 | Required                                                                             | Description                                                                          |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `BucketID`                                                                           | *string*                                                                             | :heavy_check_mark:                                                                   | ID of the bucket containing the inspected object                                     |
| `Key`                                                                                | *string*                                                                             | :heavy_check_mark:                                                                   | Key of the inspected object                                                          |
| `Versions`                                                                           | [][components.InspectObjectVersion](../../models/components/inspectobjectversion.md) | :heavy_check_mark:                                                                   | List of versions currently stored for this object                                    |