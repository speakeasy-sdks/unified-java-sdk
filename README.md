<div align="left">
    <a href="https://speakeasyapi.dev/"><img src="https://custom-icon-badges.demolab.com/badge/-Built%20By%20Speakeasy-212015?style=for-the-badge&logoColor=FBE331&logo=speakeasy&labelColor=545454" /></a>
    <a href="https://github.com/unified-to/unified-java-sdk/actions"><img src="https://img.shields.io/github/actions/workflow/status/unified-to/unified-java-sdk/sdk_generation.yaml?style=for-the-badge" /></a>
    
</div>

<!-- Start Summary [summary] -->
## Summary

The Speakeasy Bar: A bar that serves drinks.

A secret underground bar that serves drinks to those in the know.

For more information about the API: [The Speakeasy Bar Documentation.](https://docs.speakeasy.bar)
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Server Selection](#server-selection)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Asynchronous Support](#asynchronous-support)
  * [Authentication](#authentication)
  * [Custom HTTP Client](#custom-http-client)
  * [Debugging](#debugging)
  * [Jackson Configuration](#jackson-configuration)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

### Getting started

JDK 11 or later is required.

The samples below show how a published SDK artifact is used:

Gradle:
```groovy
implementation 'to.unified:unified-java-sdk:0.48.0'
```

Maven:
```xml
<dependency>
    <groupId>to.unified</groupId>
    <artifactId>unified-java-sdk</artifactId>
    <version>0.48.0</version>
</dependency>
```

### How to build
After cloning the git repository to your file system you can build the SDK artifact from source to the `build` directory by running `./gradlew build` on *nix systems or `gradlew.bat` on Windows systems.

If you wish to build from source and publish the SDK artifact to your local Maven repository (on your filesystem) then use the following command (after cloning the git repo locally):

On *nix:
```bash
./gradlew publishToMavenLocal -Pskip.signing
```
On Windows:
```bash
gradlew.bat publishToMavenLocal -Pskip.signing
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example 1

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

### Example 2

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
#### Asynchronous Call
An asynchronous SDK client is also available that returns a [`CompletableFuture<T>`][comp-fut]. See [Asynchronous Support](#asynchronous-support) for more details on async benefits and reactive library integration.
```java
package hello.world;

import java.util.concurrent.CompletableFuture;
import to.unified.unified_java_sdk.AsyncUnifiedTo;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.operations.AuthenticateRequestBody;
import to.unified.unified_java_sdk.models.operations.async.AuthenticateResponse;

public class Application {

    public static void main(String[] args) {

        AsyncUnifiedTo sdk = UnifiedTo.builder()
            .build()
            .async();

        AuthenticateRequestBody req = AuthenticateRequestBody.builder()
                .build();

        CompletableFuture<AuthenticateResponse> resFut = sdk.authentication().authenticate()
                .request(req)
                .call();

        resFut.thenAccept(res -> {
            if (res.object().isPresent()) {
                System.out.println(res.object().get());
            }
        });
    }
}
```

[comp-fut]: https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html
<!-- End SDK Example Usage [usage] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Authentication](docs/sdks/authentication/README.md)

* [authenticate](docs/sdks/authentication/README.md#authenticate) - Authenticate with the API by providing a username and password.

### [Config](docs/sdks/config/README.md)

* [subscribeToWebhooks](docs/sdks/config/README.md#subscribetowebhooks) - Subscribe to webhooks.

### [Drinks](docs/sdks/drinks/README.md)

* [getDrink](docs/sdks/drinks/README.md#getdrink) - Get a drink.
* [listDrinks](docs/sdks/drinks/README.md#listdrinks) - Get a list of drinks.

### [Food](docs/sdks/food/README.md)

* [getFood](docs/sdks/food/README.md#getfood) - Get a food item.
* [listFoods](docs/sdks/food/README.md#listfoods) - Get a list of food items.

### [Ingredients](docs/sdks/ingredients/README.md)

* [listIngredients](docs/sdks/ingredients/README.md#listingredients) - Get a list of ingredients.

### [Orders](docs/sdks/orders/README.md)

* [createOrder](docs/sdks/orders/README.md#createorder) - Create an order.

</details>
<!-- End Available Resources and Operations [operations] -->



<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Name

You can override the default server globally using the `.server(AvailableServers server)` builder method when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the names associated with the available servers:

| Name       | Server                                               | Variables                        | Description                                 |
| ---------- | ---------------------------------------------------- | -------------------------------- | ------------------------------------------- |
| `prod`     | `https://speakeasy.bar`                              |                                  | The production server.                      |
| `staging`  | `https://staging.speakeasy.bar`                      |                                  | The staging server.                         |
| `customer` | `https://{organization}.{environment}.speakeasy.bar` | `environment`<br/>`organization` | A per-organization and per-environment API. |

If the selected server has variables, you may override its default values using the associated builder method(s):

| Variable       | BuilderMethod                                | Supported Values                           | Default  | Description                                                   |
| -------------- | -------------------------------------------- | ------------------------------------------ | -------- | ------------------------------------------------------------- |
| `environment`  | `environment(ServerEnvironment environment)` | - `"prod"`<br/>- `"staging"`<br/>- `"dev"` | `"prod"` | The environment name. Defaults to the production environment. |
| `organization` | `organization(String organization)`          | java.lang.String                           | `"api"`  | The organization name. Defaults to a generic organization.    |

#### Example

```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.SDK.Builder.ServerEnvironment;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.AuthenticateRequestBody;
import to.unified.unified_java_sdk.models.operations.AuthenticateResponse;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .server(UnifiedTo.AvailableServers.CUSTOMER)
                .environment(ServerEnvironment.DEV)
                .organization("<value>")
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

### Override Server URL Per-Client

The default server can also be overridden globally using the `.serverURL(String serverUrl)` builder method when initializing the SDK client instance. For example:
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
                .serverURL("https://speakeasy.bar")
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
<!-- End Server Selection [server] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, you can provide a `RetryConfig` object through the `retryConfig` builder method:
```java
package hello.world;

import java.lang.Exception;
import java.util.concurrent.TimeUnit;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.AuthenticateRequestBody;
import to.unified.unified_java_sdk.models.operations.AuthenticateResponse;
import to.unified.unified_java_sdk.utils.BackoffStrategy;
import to.unified.unified_java_sdk.utils.RetryConfig;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
            .build();

        AuthenticateRequestBody req = AuthenticateRequestBody.builder()
                .build();

        AuthenticateResponse res = sdk.authentication().authenticate()
                .request(req)
                .retryConfig(RetryConfig.builder()
                    .backoff(BackoffStrategy.builder()
                        .initialInterval(1L, TimeUnit.MILLISECONDS)
                        .maxInterval(50L, TimeUnit.MILLISECONDS)
                        .maxElapsedTime(1000L, TimeUnit.MILLISECONDS)
                        .baseFactor(1.1)
                        .jitterFactor(0.15)
                        .retryConnectError(false)
                        .build())
                    .build())
                .call();

        if (res.object().isPresent()) {
            System.out.println(res.object().get());
        }
    }
}
```

If you'd like to override the default retry strategy for all operations that support retries, you can provide a configuration at SDK initialization:
```java
package hello.world;

import java.lang.Exception;
import java.util.concurrent.TimeUnit;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.AuthenticateRequestBody;
import to.unified.unified_java_sdk.models.operations.AuthenticateResponse;
import to.unified.unified_java_sdk.utils.BackoffStrategy;
import to.unified.unified_java_sdk.utils.RetryConfig;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .retryConfig(RetryConfig.builder()
                    .backoff(BackoffStrategy.builder()
                        .initialInterval(1L, TimeUnit.MILLISECONDS)
                        .maxInterval(50L, TimeUnit.MILLISECONDS)
                        .maxElapsedTime(1000L, TimeUnit.MILLISECONDS)
                        .baseFactor(1.1)
                        .jitterFactor(0.15)
                        .retryConnectError(false)
                        .build())
                    .build())
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
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or raise an exception.


[`UnifiedToError`](./src/main/java/models/errors/UnifiedToError.java) is the base class for all HTTP error responses. It has the following properties:

| Method           | Type                        | Description                                                              |
| ---------------- | --------------------------- | ------------------------------------------------------------------------ |
| `message()`      | `String`                    | Error message                                                            |
| `code()`         | `int`                       | HTTP response status code eg `404`                                       |
| `headers`        | `Map<String, List<String>>` | HTTP response headers                                                    |
| `body()`         | `byte[]`                    | HTTP body as a byte array. Can be empty array if no body is returned.    |
| `bodyAsString()` | `String`                    | HTTP body as a UTF-8 string. Can be empty string if no body is returned. |
| `rawResponse()`  | `HttpResponse<?>`           | Raw HTTP response (body already read and not available for re-read)      |

### Example
```java
package hello.world;

import java.io.UncheckedIOException;
import java.lang.Exception;
import java.lang.Object;
import java.lang.String;
import java.util.Map;
import java.util.Optional;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.errors.UnifiedToError;
import to.unified.unified_java_sdk.models.operations.AuthenticateRequestBody;
import to.unified.unified_java_sdk.models.operations.AuthenticateResponse;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
            .build();
        try {

            AuthenticateRequestBody req = AuthenticateRequestBody.builder()
                    .build();

            AuthenticateResponse res = sdk.authentication().authenticate()
                    .request(req)
                    .call();

            if (res.object().isPresent()) {
                System.out.println(res.object().get());
            }
        } catch (UnifiedToError ex) { // all SDK exceptions inherit from UnifiedToError

            // ex.ToString() provides a detailed error message including
            // HTTP status code, headers, and error payload (if any)
            System.out.println(ex);

            // Base exception fields
            var rawResponse = ex.rawResponse();
            var headers = ex.headers();
            var contentType = headers.first("Content-Type");
            int statusCode = ex.code();
            Optional<byte[]> responseBody = ex.body();

            // different error subclasses may be thrown 
            // depending on the service call
            if (ex instanceof APIError) {
                var e = (APIError) ex;
                // Check error data fields
                e.data().ifPresent(payload -> {
                      Optional<String> code = payload.code();
                      Optional<Map<String, Object>> details = payload.details();
                      // ...
                });
            }

            // An underlying cause may be provided. If the error payload 
            // cannot be deserialized then the deserialization exception 
            // will be set as the cause.
            if (ex.getCause() != null) {
                var cause = ex.getCause();
            }
        } catch (UncheckedIOException ex) {
            // handle IO error (connection, timeout, etc)
        }    }
}
```

### Error Classes
**Primary errors:**
* [`UnifiedToError`](./src/main/java/models/errors/UnifiedToError.java): The base class for HTTP error responses.
  * [`to.unified.unified_java_sdk.models.errors.APIError`](./src/main/java/models/errors/to.unified.unified_java_sdk.models.errors.APIError.java): An error occurred interacting with the API. Status code `5XX`.

<details><summary>Less common errors (6)</summary>

<br />

**Network errors:**
* `java.io.IOException` (always wrapped by `java.io.UncheckedIOException`). Commonly encountered subclasses of
`IOException` include `java.net.ConnectException`, `java.net.SocketTimeoutException`, `EOFException` (there are
many more subclasses in the JDK platform).

**Inherit from [`UnifiedToError`](./src/main/java/models/errors/UnifiedToError.java)**:


</details>
<!-- End Error Handling [errors] -->

<!-- Start Asynchronous Support [async-support] -->
## Asynchronous Support

The SDK provides comprehensive asynchronous support using Java's [`CompletableFuture<T>`][comp-fut] and [Reactive Streams `Publisher<T>`][reactive-streams] APIs. This design makes no assumptions about your choice of reactive toolkit, allowing seamless integration with any reactive library.

<details>
<summary>Why Use Async?</summary>

Asynchronous operations provide several key benefits:

- **Non-blocking I/O**: Your threads stay free for other work while operations are in flight
- **Better resource utilization**: Handle more concurrent operations with fewer threads
- **Improved scalability**: Build highly responsive applications that can handle thousands of concurrent requests
- **Reactive integration**: Works seamlessly with reactive streams and backpressure handling

</details>

<details>
<summary>Reactive Library Integration</summary>

The SDK returns [Reactive Streams `Publisher<T>`][reactive-streams] instances for operations dealing with streams involving multiple I/O interactions. We use Reactive Streams instead of JDK Flow API to provide broader compatibility with the reactive ecosystem, as most reactive libraries natively support Reactive Streams.

**Why Reactive Streams over JDK Flow?**
- **Broader ecosystem compatibility**: Most reactive libraries (Project Reactor, RxJava, Akka Streams, etc.) natively support Reactive Streams
- **Industry standard**: Reactive Streams is the de facto standard for reactive programming in Java
- **Better interoperability**: Seamless integration without additional adapters for most use cases

**Integration with Popular Libraries:**
- **Project Reactor**: Use `Flux.from(publisher)` to convert to Reactor types
- **RxJava**: Use `Flowable.fromPublisher(publisher)` for RxJava integration
- **Akka Streams**: Use `Source.fromPublisher(publisher)` for Akka Streams integration
- **Vert.x**: Use `ReadStream.fromPublisher(vertx, publisher)` for Vert.x reactive streams
- **Mutiny**: Use `Multi.createFrom().publisher(publisher)` for Quarkus Mutiny integration

**For JDK Flow API Integration:**
If you need JDK Flow API compatibility (e.g., for Quarkus/Mutiny 2), you can use adapters:
```java
// Convert Reactive Streams Publisher to Flow Publisher
Flow.Publisher<T> flowPublisher = FlowAdapters.toFlowPublisher(reactiveStreamsPublisher);

// Convert Flow Publisher to Reactive Streams Publisher
Publisher<T> reactiveStreamsPublisher = FlowAdapters.toPublisher(flowPublisher);
```

For standard single-response operations, the SDK returns `CompletableFuture<T>` for straightforward async execution.

</details>

<details>
<summary>Supported Operations</summary>

Async support is available for:

- **[Server-sent Events](#server-sent-event-streaming)**: Stream real-time events with Reactive Streams `Publisher<T>`
- **[JSONL Streaming](#jsonl-streaming)**: Process streaming JSON lines asynchronously
- **[Pagination](#pagination)**: Iterate through paginated results using `callAsPublisher()` and `callAsPublisherUnwrapped()`
- **[File Uploads](#file-uploads)**: Upload files asynchronously with progress tracking
- **[File Downloads](#file-downloads)**: Download files asynchronously with streaming support
- **[Standard Operations](#example)**: All regular API calls return `CompletableFuture<T>` for async execution

</details>

[comp-fut]: https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html
[reactive-streams]: https://www.reactive-streams.org/
<!-- End Asynchronous Support [async-support] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security schemes globally:

| Name                | Type   | Scheme       |
| ------------------- | ------ | ------------ |
| `apiKey`            | apiKey | API key      |
| `clientCredentials` | oauth2 | OAuth2 token |

You can set the security parameters through the `security` builder method when initializing the SDK client instance. The selected scheme will be used by default to authenticate with the API for all operations that support it. For example:
```java
package hello.world;

import java.lang.Exception;
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.models.errors.APIError;
import to.unified.unified_java_sdk.models.operations.AuthenticateRequestBody;
import to.unified.unified_java_sdk.models.operations.AuthenticateResponse;
import to.unified.unified_java_sdk.models.shared.Security;

public class Application {

    public static void main(String[] args) throws APIError, Exception {

        UnifiedTo sdk = UnifiedTo.builder()
                .security(Security.builder()
                    .apiKey(System.getenv().getOrDefault("API_KEY", ""))
                    .build())
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
<!-- End Authentication [security] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Java SDK makes API calls using an `HTTPClient` that wraps the native
[HttpClient](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html). This
client provides the ability to attach hooks around the request lifecycle that can be used to modify the request or handle
errors and response.

The `HTTPClient` interface allows you to either use the default `SpeakeasyHTTPClient` that comes with the SDK,
or provide your own custom implementation with customized configuration such as custom executors, SSL context,
connection pools, and other HTTP client settings.

The interface provides synchronous (`send`) methods and asynchronous (`sendAsync`) methods. The `sendAsync` method
is used to power the async SDK methods and returns a `CompletableFuture<HttpResponse<Blob>>` for non-blocking operations.

The following example shows how to add a custom header and handle errors:

```java
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.utils.HTTPClient;
import to.unified.unified_java_sdk.utils.SpeakeasyHTTPClient;
import to.unified.unified_java_sdk.utils.Utils;

import java.io.IOException;
import java.net.URISyntaxException;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.InputStream;
import java.time.Duration;

public class Application {
    public static void main(String[] args) {
        // Create a custom HTTP client with hooks
        HTTPClient httpClient = new HTTPClient() {
            private final HTTPClient defaultClient = new SpeakeasyHTTPClient();
            
            @Override
            public HttpResponse<InputStream> send(HttpRequest request) throws IOException, URISyntaxException, InterruptedException {
                // Add custom header and timeout using Utils.copy()
                HttpRequest modifiedRequest = Utils.copy(request)
                    .header("x-custom-header", "custom value")
                    .timeout(Duration.ofSeconds(30))
                    .build();
                    
                try {
                    HttpResponse<InputStream> response = defaultClient.send(modifiedRequest);
                    // Log successful response
                    System.out.println("Request successful: " + response.statusCode());
                    return response;
                } catch (Exception error) {
                    // Log error
                    System.err.println("Request failed: " + error.getMessage());
                    throw error;
                }
            }
        };

        UnifiedTo sdk = UnifiedTo.builder()
            .client(httpClient)
            .build();
    }
}
```

<details>
<summary>Custom HTTP Client Configuration</summary>

You can also provide a completely custom HTTP client with your own configuration:

```java
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.utils.HTTPClient;
import to.unified.unified_java_sdk.utils.Blob;
import to.unified.unified_java_sdk.utils.ResponseWithBody;

import java.io.IOException;
import java.net.URISyntaxException;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.InputStream;
import java.time.Duration;
import java.util.concurrent.Executors;
import java.util.concurrent.CompletableFuture;

public class Application {
    public static void main(String[] args) {
        // Custom HTTP client with custom configuration
        HTTPClient customHttpClient = new HTTPClient() {
            private final HttpClient client = HttpClient.newBuilder()
                .executor(Executors.newFixedThreadPool(10))
                .connectTimeout(Duration.ofSeconds(30))
                // .sslContext(customSslContext) // Add custom SSL context if needed
                .build();

            @Override
            public HttpResponse<InputStream> send(HttpRequest request) throws IOException, URISyntaxException, InterruptedException {
                return client.send(request, HttpResponse.BodyHandlers.ofInputStream());
            }

            @Override
            public CompletableFuture<HttpResponse<Blob>> sendAsync(HttpRequest request) {
                // Convert response to HttpResponse<Blob> for async operations
                return client.sendAsync(request, HttpResponse.BodyHandlers.ofPublisher())
                    .thenApply(resp -> new ResponseWithBody<>(resp, Blob::from));
            }
        };

        UnifiedTo sdk = UnifiedTo.builder()
            .client(customHttpClient)
            .build();
    }
}
```

</details>

You can also enable debug logging on the default `SpeakeasyHTTPClient`:

```java
import to.unified.unified_java_sdk.UnifiedTo;
import to.unified.unified_java_sdk.utils.SpeakeasyHTTPClient;

public class Application {
    public static void main(String[] args) {
        SpeakeasyHTTPClient httpClient = new SpeakeasyHTTPClient();
        httpClient.enableDebugLogging(true);

        UnifiedTo sdk = UnifiedTo.builder()
            .client(httpClient)
            .build();
    }
}
```
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Debugging [debug] -->
## Debugging

### Debug

You can setup your SDK to emit debug logs for SDK requests and responses.

For request and response logging (especially json bodies), call `enableHTTPDebugLogging(boolean)` on the SDK builder like so:

```java
SDK.builder()
    .enableHTTPDebugLogging(true)
    .build();
```
Example output:
```
Sending request: http://localhost:35123/bearer#global GET
Request headers: {Accept=[application/json], Authorization=[******], Client-Level-Header=[added by client], Idempotency-Key=[some-key], x-speakeasy-user-agent=[speakeasy-sdk/java 0.0.1 internal 0.1.0 org.openapis.openapi]}
Received response: (GET http://localhost:35123/bearer#global) 200
Response headers: {access-control-allow-credentials=[true], access-control-allow-origin=[*], connection=[keep-alive], content-length=[50], content-type=[application/json], date=[Wed, 09 Apr 2025 01:43:29 GMT], server=[gunicorn/19.9.0]}
Response body:
{
  "authenticated": true, 
  "token": "global"
}
```
__WARNING__: This logging should only be used for temporary debugging purposes. Leaving this option on in a production system could expose credentials/secrets in logs. <i>Authorization</i> headers are redacted by default and there is the ability to specify redacted header names via `SpeakeasyHTTPClient.setRedactedHeaders`.

__NOTE__: This is a convenience method that calls `HTTPClient.enableDebugLogging()`. The `SpeakeasyHTTPClient` honors this setting. If you are using a custom HTTP client, it is up to the custom client to honor this setting.


Another option is to set the System property `-Djdk.httpclient.HttpClient.log=all`. However, this second option does not log bodies.
<!-- End Debugging [debug] -->

<!-- Start Jackson Configuration [jackson] -->
## Jackson Configuration

The SDK ships with a pre-configured Jackson [`ObjectMapper`][jackson-databind] accessible via
`JSON.getMapper()`. It is set up with type modules, strict deserializers, and the feature flags
needed for full SDK compatibility (including ISO-8601 `OffsetDateTime` serialization):

```java
import to.unified.unified_java_sdk.utils.JSON;

String json = JSON.getMapper().writeValueAsString(response);
```

To compose with your own `ObjectMapper`, register the provided `UnifiedJavaSDKJacksonModule`, which
bundles all the same modules and feature flags as a single plug-and-play module:

```java
import to.unified.unified_java_sdk.utils.UnifiedJavaSDKJacksonModule;
import com.fasterxml.jackson.databind.ObjectMapper;

ObjectMapper myMapper = new ObjectMapper()
    .registerModule(new UnifiedJavaSDKJacksonModule());

String json = myMapper.writeValueAsString(response);
```

[jackson-databind]: https://github.com/FasterXML/jackson-databind
[jackson-jsr310]: https://github.com/FasterXML/jackson-modules-java8/tree/master/datetime
<!-- End Jackson Configuration [jackson] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->



### Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

### Contributions

While we value open-source contributions to this SDK, this library is generated programmatically.
Feel free to open a PR or a Github issue as a proof of concept and we'll do our best to include it in a future release!

### SDK Created by [Speakeasy](https://docs.speakeasyapi.dev/docs/using-speakeasy/client-sdks)
