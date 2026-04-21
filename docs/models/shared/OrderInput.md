# OrderInput

An order for a drink or ingredient.


## Fields

| Field                                                                             | Type                                                                              | Required                                                                          | Description                                                                       | Example                                                                           |
| --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `productCode`                                                                     | *String*                                                                          | :heavy_check_mark:                                                                | The product code of the drink or ingredient.                                      | **Example 1:** AC-A2DF3<br/>**Example 2:** NAC-3F2D1<br/>**Example 3:** APM-1F2D3 |
| `quantity`                                                                        | *long*                                                                            | :heavy_check_mark:                                                                | The number of units of the drink or ingredient to order.                          |                                                                                   |
| `type`                                                                            | [OrderType](../../models/shared/OrderType.md)                                     | :heavy_check_mark:                                                                | The type of order.                                                                |                                                                                   |