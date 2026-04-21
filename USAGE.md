<!-- Start SDK Example Usage [usage] -->
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
<!-- End SDK Example Usage [usage] -->