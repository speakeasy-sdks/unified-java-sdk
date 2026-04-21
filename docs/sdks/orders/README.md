# Orders

## Overview

The orders endpoints.

### Available Operations

* [createOrder](#createorder) - Create an order.

## createOrder

Create an order for a drink.

### Example Usage

<!-- UsageSnippet language="java" operationID="createOrder" method="post" path="/order" -->
```java
package hello.world;

import java.lang.Exception;
import java.util.List;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.CreateOrderRequest;
import to.unified.unified_java_sdk.models.operations.CreateOrderResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .apiKey(System.getenv().getOrDefault("API_KEY", ""))
                    .build())
            .build();

        CreateOrderRequest req = CreateOrderRequest.builder()
                .requestBody(List.of())
                .build();

        CreateOrderResponse res = sdk.orders().createOrder()
                .request(req)
                .call();

        if (res.order().isPresent()) {
            System.out.println(res.order().get());
        }
    }
}
```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [CreateOrderRequest](../../models/operations/CreateOrderRequest.md) | :heavy_check_mark:                                                  | The request object to use for the request.                          |

### Response

**[CreateOrderResponse](../../models/operations/CreateOrderResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |