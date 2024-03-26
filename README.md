# Microservices Deployment Configuration

This repository contains the deployment configuration for a set of microservices using Kubernetes.

## Services

### Email Service

- **Image:** gcr.io/google-samples/microservices-demo/emailservice:v0.2.3
- **Ports:** 8080
- **Environment Variables:** PORT=8080, DISABLE_TRACING=1, DISABLE_PROFILER=1
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:8080` every 5 seconds
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:8080` every 5 seconds
- **Resources:** Requests 100m CPU and 64Mi memory, limits 200m CPU and 128Mi memory

### Recommendation Service

- **Image:** gcr.io/google-samples/microservices-demo/recommendationservice:v0.2.3
- **Ports:** 8080
- **Environment Variables:** PORT=8080, PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550, DISABLE_TRACING=1, DISABLE_PROFILER=1, DISABLE_DEBUGGER=1
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:8080` every 5 seconds
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:8080` every 5 seconds
- **Resources:** Requests 100m CPU and 220Mi memory, limits 200m CPU and 450Mi memory

### Payment Service

- **Image:** gcr.io/google-samples/microservices-demo/paymentservice:v0.2.3
- **Ports:** 50051
- **Environment Variables:** PORT=50051
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:50051`
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:50051`
- **Resources:** Requests 100m CPU and 64Mi memory, limits 200m CPU and 128Mi memory

### Product Catalog Service

- **Image:** gcr.io/google-samples/microservices-demo/productcatalogservice:v0.2.3
- **Ports:** 3550
- **Environment Variables:** PORT=3550
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:3550`
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:3550`
- **Resources:** Requests 100m CPU and 64Mi memory, limits 200m CPU and 128Mi memory

### Currency Service

- **Image:** gcr.io/google-samples/microservices-demo/currencyservice:v0.2.3
- **Ports:** 7000
- **Environment Variables:** PORT=7000
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:7000`
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:7000`
- **Resources:** Requests 100m CPU and 64Mi memory, limits 200m CPU and 128Mi memory

### Shipping Service

- **Image:** gcr.io/google-samples/microservices-demo/shippingservice:v0.2.3
- **Ports:** 50051
- **Environment Variables:** PORT=50051
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:50051`
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:50051`
- **Resources:** Requests 100m CPU and 64Mi memory, limits 200m CPU and 128Mi memory

### Ad Service

- **Image:** gcr.io/google-samples/microservices-demo/adservice:v0.2.3
- **Ports:** 9555
- **Environment Variables:** PORT=9555
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:9555`
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:9555`
- **Resources:** Requests 200m CPU and 180Mi memory, limits 300m CPU and 300Mi memory

### Cart Service

- **Image:** gcr.io/google-samples/microservices-demo/cartservice:v0.2.3
- **Ports:** 7070
- **Environment Variables:** REDIS_ADDR=redis-cart:6379
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:7070 -rpc-timeout=5s` after an initial delay of 15 seconds
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:7070 -rpc-timeout=5s` after an initial delay of 15 seconds
- **Resources:** Requests 200m CPU and 64Mi memory, limits 300m CPU and 128Mi memory

### Checkout Service

- **Image:** gcr.io/google-samples/microservices-demo/checkoutservice:v0.2.3
- **Ports:** 5050
- **Environment Variables:** PORT=5050, PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550, SHIPPING_SERVICE_ADDR=shippingservice:50051, PAYMENT_SERVICE_ADDR=paymentservice:50051, EMAIL_SERVICE_ADDR=emailservice:5000, CURRENCY_SERVICE_ADDR=currencyservice:7000, CART_SERVICE_ADDR=cartservice:7070
- **Readiness Probe:** Executes `/bin/grpc_health_probe -addr=:5050`
- **Liveness Probe:** Executes `/bin/grpc_health_probe -addr=:5050`
- **Resources:** Requests 100m CPU and 64Mi memory, limits 200m CPU and 128Mi memory

### Frontend Service

- **Image:** gcr.io/google-samples/microservices-demo/frontend:v0.2.3
- **Ports:** 8080
- **Environment Variables:** PORT=8080, PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550, CURRENCY_SERVICE_ADDR=currencyservice:7000, CART_SERVICE_ADDR=cartservice:7070, RECOMMENDATION_SERVICE_ADDR=recommendationservice:8080, SHIPPING_SERVICE_ADDR=shippingservice:50051, CHECKOUT_SERVICE_ADDR=checkoutservice:5050, AD_SERVICE_ADDR=adservice:9555
- **Readiness Probe:** Executes `http GET /_healthz` on port 8080 with a cookie `

# Online Shop Microservices Helm Chart

This Helm chart deploys a set of microservices for an online shop using Kubernetes. The microservices include `emailservice`, `recommendationservice`, `paymentservice`, `productcatalogservice`, `currencyservice`, `shippingservice`, `adservice`, `cartservice`, `checkoutservice`, and `frontend`.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+

## Installation

### Clone the Helm chart repository:

```bash
git clone https://github.com/ilem0na/online-shop-microservices.git
```

1. Install the chart with the release name my-release:

   ```bash
   helm install my-release ./online-shop-microservices
   ```

   The command deploys the online shop microservices chart on the Kubernetes cluster in the default configuration.

   Uninstallation
   To uninstall/delete the my-release deployment:

   ```bash
   helm uninstall my-release
   ```

## Configuration

The following table lists the configurable parameters of the online shop microservices chart and their default values.

| Parameter                     | Description                                   | Default                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `emailservice.image`          | Email service image                           | `gcr.io/google-samples/microservices-demo/emailservice:v0.2.3`                                                                                                                                                                                                                                                                                                |
| `emailservice.port`           | Email service port                            | `8080`                                                                                                                                                                                                                                                                                                                                                        |
| `emailservice.env`            | Email service environment variables           | `PORT: '8080', DISABLE_TRACING: '1', DISABLE_PROFILER: '1'`                                                                                                                                                                                                                                                                                                   |
| `recommendationservice.image` | Recommendation service image                  | `gcr.io/google-samples/microservices-demo/recommendationservice:v0.2.3`                                                                                                                                                                                                                                                                                       |
| `recommendationservice.port`  | Recommendation service port                   | `8080`                                                                                                                                                                                                                                                                                                                                                        |
| `recommendationservice.env`   | Recommendation service environment variables  | `PORT: '8080', PRODUCT_CATALOG_SERVICE_ADDR: 'productcatalogservice:3550', DISABLE_TRACING: '1', DISABLE_PROFILER: '1', DISABLE_DEBUGGER: '1'`                                                                                                                                                                                                                |
| `paymentservice.image`        | Payment service image                         | `gcr.io/google-samples/microservices-demo/paymentservice:v0.2.3`                                                                                                                                                                                                                                                                                              |
| `paymentservice.port`         | Payment service port                          | `50051`                                                                                                                                                                                                                                                                                                                                                       |
| `paymentservice.env`          | Payment service environment variables         | `PORT: '50051'`                                                                                                                                                                                                                                                                                                                                               |
| `productcatalogservice.image` | Product catalog service image                 | `gcr.io/google-samples/microservices-demo/productcatalogservice:v0.2.3`                                                                                                                                                                                                                                                                                       |
| `productcatalogservice.port`  | Product catalog service port                  | `3550`                                                                                                                                                                                                                                                                                                                                                        |
| `productcatalogservice.env`   | Product catalog service environment variables | `PORT: '3550'`                                                                                                                                                                                                                                                                                                                                                |
| `currencyservice.image`       | Currency service image                        | `gcr.io/google-samples/microservices-demo/currencyservice:v0.2.3`                                                                                                                                                                                                                                                                                             |
| `currencyservice.port`        | Currency service port                         | `7000`                                                                                                                                                                                                                                                                                                                                                        |
| `currencyservice.env`         | Currency service environment variables        | `PORT: '7000'`                                                                                                                                                                                                                                                                                                                                                |
| `shippingservice.image`       | Shipping service image                        | `gcr.io/google-samples/microservices-demo/shippingservice:v0.2.3`                                                                                                                                                                                                                                                                                             |
| `shippingservice.port`        | Shipping service port                         | `50051`                                                                                                                                                                                                                                                                                                                                                       |
| `shippingservice.env`         | Shipping service environment variables        | `PORT: '50051'`                                                                                                                                                                                                                                                                                                                                               |
| `adservice.image`             | Ad service image                              | `gcr.io/google-samples/microservices-demo/adservice:v0.2.3`                                                                                                                                                                                                                                                                                                   |
| `adservice.port`              | Ad service port                               | `9555`                                                                                                                                                                                                                                                                                                                                                        |
| `adservice.env`               | Ad service environment variables              | `PORT: '9555'`                                                                                                                                                                                                                                                                                                                                                |
| `cartservice.image`           | Cart service image                            | `gcr.io/google-samples/microservices-demo/cartservice:v0.2.3`                                                                                                                                                                                                                                                                                                 |
| `cartservice.port`            | Cart service port                             | `7070`                                                                                                                                                                                                                                                                                                                                                        |
| `cartservice.env`             | Cart service environment variables            | `REDIS_ADDR: 'redis-cart:6379'`                                                                                                                                                                                                                                                                                                                               |
| `checkoutservice.image`       | Checkout service image                        | `gcr.io/google-samples/microservices-demo/checkoutservice:v0.2.3`                                                                                                                                                                                                                                                                                             |
| `checkoutservice.port`        | Checkout service port                         | `5050`                                                                                                                                                                                                                                                                                                                                                        |
| `checkoutservice.env`         | Checkout service environment variables        | `PORT: '5050', PRODUCT_CATALOG_SERVICE_ADDR: 'productcatalogservice:3550', SHIPPING_SERVICE_ADDR: 'shippingservice:50051', PAYMENT_SERVICE_ADDR: 'paymentservice:50051', EMAIL_SERVICE_ADDR: 'emailservice:5000', CURRENCY_SERVICE_ADDR: 'currencyservice:7000', CART_SERVICE_ADDR: 'cartservice:7070'`                                                       |
| `frontend.image`              | Frontend image                                | `gcr.io/google-samples/microservices-demo/frontend:v0.2.3`                                                                                                                                                                                                                                                                                                    |
| `frontend.port`               | Frontend port                                 | `8080`                                                                                                                                                                                                                                                                                                                                                        |
| `frontend.env`                | Frontend environment variables                | `PORT: '8080', PRODUCT_CATALOG_SERVICE_ADDR: 'productcatalogservice:3550', CURRENCY_SERVICE_ADDR: 'currencyservice:7000', CART_SERVICE_ADDR: 'cartservice:7070', RECOMMENDATION_SERVICE_ADDR: 'recommendationservice:8080', SHIPPING_SERVICE_ADDR: 'shippingservice:50051', CHECKOUT_SERVICE_ADDR: 'checkoutservice:5050', AD_SERVICE_ADDR: 'adservice:9555'` |
