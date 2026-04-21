# Authentication

## Overview

The authentication endpoints.

### Available Operations

* [authenticate](#authenticate) - Authenticate with the API by providing a username and password.

## authenticate

Authenticate with the API by providing a username and password.

### Example Usage

<!-- UsageSnippet language="java" operationID="authenticate" method="post" path="/authenticate" -->
```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.AuthenticateRequestBody;
import to.unified.unified_java_sdk.models.operations.AuthenticateResponse;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
            .build();

        AuthenticateRequestBody req = AuthenticateRequestBody.builder()
                .build();

        AuthenticateResponse res = sdk.authentication().authenticate()
                .request(req)
                .call();

        if (res.object().isPresent()) {
            System.out.println(res.object().get());
        }
    }
}
```

### Parameters

| Parameter                                                                     | Type                                                                          | Required                                                                      | Description                                                                   |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `request`                                                                     | [AuthenticateRequestBody](../../models/operations/AuthenticateRequestBody.md) | :heavy_check_mark:                                                            | The request object to use for the request.                                    |

### Response

**[AuthenticateResponse](../../models/operations/AuthenticateResponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| models/errors/APIError | 5XX                    | application/json       |
| models/errors/SDKError | 4XX                    | \*/\*                  |