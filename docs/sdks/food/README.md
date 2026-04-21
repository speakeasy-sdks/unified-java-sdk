# Food

## Overview

The food endpoints.

### Available Operations

* [getFood](#getfood) - Get a food item.
* [listFoods](#listfoods) - Get a list of food items.

## getFood

Get a food item by name.

### Example Usage

<!-- UsageSnippet language="java" operationID="getFood" method="get" path="/food/{name}" -->
```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.GetFoodRequest;
import to.unified.unified_java_sdk.models.operations.GetFoodResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .apiKey(System.getenv().getOrDefault("API_KEY", ""))
                    .build())
            .build();

        GetFoodRequest req = GetFoodRequest.builder()
                .name("<value>")
                .build();

        GetFoodResponse res = sdk.food().getFood()
                .request(req)
                .call();

        if (res.object().isPresent()) {
            System.out.println(res.object().get());
        }
    }
}
```

### Parameters

| Parameter                                                   | Type                                                        | Required                                                    | Description                                                 |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `request`                                                   | [GetFoodRequest](../../models/operations/GetFoodRequest.md) | :heavy_check_mark:                                          | The request object to use for the request.                  |

### Response

**[GetFoodResponse](../../models/operations/GetFoodResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |

## listFoods

Get a list of food items.

### Example Usage

<!-- UsageSnippet language="java" operationID="listFoods" method="get" path="/foods" -->
```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.ListFoodsResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .apiKey(System.getenv().getOrDefault("API_KEY", ""))
                    .build())
            .build();

        ListFoodsResponse res = sdk.food().listFoods()
                .call();

        if (res.object().isPresent()) {
            System.out.println(res.object().get());
        }
    }
}
```

### Response

**[ListFoodsResponse](../../models/operations/ListFoodsResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |