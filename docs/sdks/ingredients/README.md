# Ingredients

## Overview

The ingredients endpoints.

### Available Operations

* [listIngredients](#listingredients) - Get a list of ingredients.

## listIngredients

Get a list of ingredients, if authenticated this will include stock levels and product codes otherwise it will only include public information.

### Example Usage

<!-- UsageSnippet language="java" operationID="listIngredients" method="get" path="/ingredients" -->
```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.ListIngredientsRequest;
import to.unified.unified_java_sdk.models.operations.ListIngredientsResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .apiKey(System.getenv().getOrDefault("API_KEY", ""))
                    .build())
            .build();

        ListIngredientsRequest req = ListIngredientsRequest.builder()
                .page(982293L)
                .build();

        ListIngredientsResponse res = sdk.ingredients().listIngredients()
                .request(req)
                .call();

        if (res.object().isPresent()) {
            System.out.println(res.object().get());
        }
    }
}
```

### Parameters

| Parameter                                                                   | Type                                                                        | Required                                                                    | Description                                                                 |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `request`                                                                   | [ListIngredientsRequest](../../models/operations/ListIngredientsRequest.md) | :heavy_check_mark:                                                          | The request object to use for the request.                                  |

### Response

**[ListIngredientsResponse](../../models/operations/ListIngredientsResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |