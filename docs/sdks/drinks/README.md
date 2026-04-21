# Drinks

## Overview

The drinks endpoints.

### Available Operations

* [getDrink](#getdrink) - Get a drink.
* [listDrinks](#listdrinks) - Get a list of drinks.

## getDrink

Get a drink by name, if authenticated this will include stock levels and product codes otherwise it will only include public information.

### Example Usage

<!-- UsageSnippet language="java" operationID="getDrink" method="get" path="/drink/{name}" -->
```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.GetDrinkRequest;
import to.unified.unified_java_sdk.models.operations.GetDrinkResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .apiKey(System.getenv().getOrDefault("API_KEY", ""))
                    .build())
            .build();

        GetDrinkRequest req = GetDrinkRequest.builder()
                .name("<value>")
                .build();

        GetDrinkResponse res = sdk.drinks().getDrink()
                .request(req)
                .call();

        if (res.drink().isPresent()) {
            System.out.println(res.drink().get());
        }
    }
}
```

### Parameters

| Parameter                                                     | Type                                                          | Required                                                      | Description                                                   |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `request`                                                     | [GetDrinkRequest](../../models/operations/GetDrinkRequest.md) | :heavy_check_mark:                                            | The request object to use for the request.                    |

### Response

**[GetDrinkResponse](../../models/operations/GetDrinkResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |

## listDrinks

Get a list of drinks, if authenticated this will include stock levels and product codes otherwise it will only include public information.

### Example Usage

<!-- UsageSnippet language="java" operationID="listDrinks" method="get" path="/drinks" -->
```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.ListDrinksResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .clientCredentials(System.getenv().getOrDefault("CLIENT_CREDENTIALS", ""))
                    .build())
            .build();

        ListDrinksResponse res = sdk.drinks().listDrinks()
                .call();

        if (res.drinks().isPresent()) {
            System.out.println(res.drinks().get());
        }
    }
}
```

### Parameters

| Parameter                                                         | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `request`                                                         | [ListDrinksRequest](../../models/operations/ListDrinksRequest.md) | :heavy_check_mark:                                                | The request object to use for the request.                        |

### Response

**[ListDrinksResponse](../../models/operations/ListDrinksResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |