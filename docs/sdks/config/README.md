# Config

## Overview

### Available Operations

* [subscribeToWebhooks](#subscribetowebhooks) - Subscribe to webhooks.

## subscribeToWebhooks

Subscribe to webhooks.

### Example Usage

<!-- UsageSnippet language="java" operationID="subscribeToWebhooks" method="post" path="/webhooks/subscribe" -->
```java
package hello.world;

import java.lang.Exception;
import java.util.List;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.RequestBody;
import to.unified.unified_java_sdk.models.operations.SubscribeToWebhooksResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .apiKey(System.getenv().getOrDefault("API_KEY", ""))
                    .build())
            .build();

        List<RequestBody> req = List.of();

        SubscribeToWebhooksResponse res = sdk.config().subscribeToWebhooks()
                .request(req)
                .call();

        if (res.error().isPresent()) {
            System.out.println(res.error().get());
        }
    }
}
```

### Parameters

| Parameter                                  | Type                                       | Required                                   | Description                                |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| `request`                                  | [List<RequestBody>](../../models//.md)     | :heavy_check_mark:                         | The request object to use for the request. |

### Response

**[SubscribeToWebhooksResponse](../../models/operations/SubscribeToWebhooksResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |