# Microservices Deployment Configuration

This repository contains the deployment configuration for a set of microservices using Kubernetes.

## Services

### Email Service

- **Image:** gcr.io/google-samples/microservices-demo/emailservice:v0.2.3
- **Ports:** 8080
- **Environment Variables:** PORT=8080

### Recommendation Service

- **Image:** gcr.io/google-samples/microservices-demo/recommendationservice:v0.2.3
- **Ports:** 8080
- **Environment Variables:** PORT=8080, PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550

### Product Catalog Service

- **Image:** gcr.io/google-samples/microservices-demo/productcatalogservice:v0.2.3
- **Ports:** 3550
- **Environment Variables:** PORT=3550

### Payment Service

- **Image:** gcr.io/google-samples/microservices-demo/paymentservice:v0.2.3
- **Ports:** 50051
- **Environment Variables:** PORT=50051, GOOGLE_CLOUD_PROJECT=ilemona-vm

### Currency Service

- **Image:** gcr.io/google-samples/microservices-demo/currencyservice:v0.2.3
- **Ports:** 7000
- **Environment Variables:** PORT=7000, GOOGLE_CLOUD_PROJECT=ilemona-vm

### Shipping Service

- **Image:** gcr.io/google-samples/microservices-demo/shippingservice:v0.2.3
- **Ports:** 50051
- **Environment Variables:** PORT=50051

### Ad Service

- **Image:** gcr.io/google-samples/microservices-demo/adservice:v0.3.7
- **Ports:** 9555
- **Environment Variables:** PORT=9555

### Cart Service

- **Image:** gcr.io/google-samples/microservices-demo/cartservice:v0.2.3
- **Ports:** 7070
- **Environment Variables:** REDIS_ADDR=redis-cart:6379

### Checkout Service

- **Image:** gcr.io/google-samples/microservices-demo/checkoutservice:v0.2.3
- **Ports:** 5050
- **Environment Variables:** PORT=5050, PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550, SHIPPING_SERVICE_ADDR=shippingservice:50051, PAYMENT_SERVICE_ADDR=paymentservice:50051, EMAIL_SERVICE_ADDR=emailservice:5000, CURRENCY_SERVICE_ADDR=currencyservice:7000, CART_SERVICE_ADDR=cartservice:7070

### Frontend Service

- **Image:** gcr.io/google-samples/microservices-demo/frontend:v0.2.3
- **Ports:** 8080
- **Environment Variables:** PORT=8080, PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550, CURRENCY_SERVICE_ADDR=currencyservice:7000, CART_SERVICE_ADDR=cartservice:7070, RECOMMENDATION_SERVICE_ADDR=recommendationservice:8080, SHIPPING_SERVICE_ADDR=shippingservice:50051, CHECKOUT_SERVICE_ADDR=checkoutservice:5050, AD_SERVICE_ADDR=adservice:9555

## Deployment

The deployment configuration for each service is defined in the corresponding YAML files in this repository. You can deploy these services using Kubernetes.

## Service Discovery

Services can discover and communicate with each other using their service names. For example, the Checkout Service can communicate with the Payment Service using the address `paymentservice:50051`.
