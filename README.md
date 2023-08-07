## Architecture

**Online Boutique** is composed of 11 microservices written in different
languages that talk to each other over gRPC.

[![Architecture of
microservices](/docs/img/architecture-diagram.png)](/docs/img/architecture-diagram.png)

Find **Protocol Buffers Descriptions** at the [`./protos` directory](/protos).

| Service                                              | Language      | Description                                                                                                                       |
| ---------------------------------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [frontend](google-cloud-microservices-demo/microservices-demo/src/frontend)                           | Go            | Exposes an HTTP server to serve the website. Does not require signup/login and generates session IDs for all users automatically. |
| [cartservice](google-cloud-microservices-demo/microservices-demo/src/cartservice)                     | C#            | Stores the items in the user's shopping cart in Redis and retrieves it.                                                           |
| [productcatalogservice](google-cloud-microservices-demo/microservices-demo/src/productcatalogservice) | Go            | Provides the list of products from a JSON file and ability to search products and get individual products.                        |
| [currencyservice](google-cloud-microservices-demo/microservices-demo/src/currencyservice)             | Node.js       | Converts one money amount to another currency. Uses real values fetched from European Central Bank. It's the highest QPS service. |
| [paymentservice](google-cloud-microservices-demo/microservices-demo/src/paymentservice)               | Node.js       | Charges the given credit card info (mock) with the given amount and returns a transaction ID.                                     |
| [shippingservice](google-cloud-microservices-demo/microservices-demo/src/shippingservice)             | Go            | Gives shipping cost estimates based on the shopping cart. Ships items to the given address (mock)                                 |
| [emailservice](google-cloud-microservices-demo/microservices-demo/src/emailservice)                   | Python        | Sends users an order confirmation email (mock).                                                                                   |
| [checkoutservice](google-cloud-microservices-demo/microservices-demo/src/checkoutservice)             | Go            | Retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification.                            |
| [recommendationservice](google-cloud-microservices-demo/microservices-demo/src/recommendationservice) | Python        | Recommends other products based on what's given in the cart.                                                                      |
| [adservice](google-cloud-microservices-demo/microservices-demo/src/adservice)                         | Java          | Provides text ads based on given context words.                                                                                   |
| [loadgenerator](google-cloud-microservices-demo/microservices-demo/src/loadgenerator)                 | Python/Locust | Continuously sends requests imitating realistic user shopping flows to the frontend.                                              |