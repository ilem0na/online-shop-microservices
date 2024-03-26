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
