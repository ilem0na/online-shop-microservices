# online-shop-microservices

This repository contains a set of Kubernetes manifests for deploying a microservices-based application demo. The demo consists of several microservices, each serving a specific function, such as email service, recommendation service, product catalog service, payment service, and more. Below are the details of the services and how to deploy them using Kubernetes.

Services Overview
Email Service

Image: gcr.io/google-samples/microservices-demo/emailservice:v0.9.0
Port: 8080
Environment variable: PORT=8080
Recommendation Service

Image: gcr.io/google-samples/microservices-demo/recommendationservice:v0.3.6-issue2367
Port: 8080
Environment variables:
PORT=8080
PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550
Product Catalog Service

Image: gcr.io/google-samples/microservices-demo/productcatalogservice:v0.9.0
Port: 3550
Environment variable: PORT=3550
Payment Service

Image: gcr.io/google-samples/microservices-demo/paymentservice:v0.9.0
Port: 50051
Environment variable: PORT=50051
Currency Service

Image: gcr.io/google-samples/microservices-demo/currencyservice:v0.9.0
Port: 7000
Environment variable: PORT=7000
Shipping Service

Image: gcr.io/google-samples/microservices-demo/shippingservice:v0.9.0
Port: 50051
Environment variable: PORT=50051
Ad Service

Image: gcr.io/google-samples/microservices-demo/adservice:v0.9.0
Port: 9555
Environment variable: PORT=9555
Cart Service

Image: gcr.io/google-samples/microservices-demo/cartservice:v0.9.0
Port: 7070
Environment variable: REDIS_ADDR=redis-cart:6379
Checkout Service

Image: gcr.io/google-samples/microservices-demo/checkoutservice:v0.9.0
Port: 5050
Environment variables:
PORT=5050
PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550
SHIPPING_SERVICE_ADDR=shippingservice:50051
PAYMENT_SERVICE_ADDR=paymentservice:50051
EMAIL_SERVICE_ADDR=emailservice:5000
CURRENCY_SERVICE_ADDR=currencyservice:7000
CART_SERVICE_ADDR=cartservice:7070
Frontend Service

Image: gcr.io/google-samples/microservices-demo/frontend:v0.9.0
Port: 8080
Environment variables:
PORT=8080
PRODUCT_CATALOG_SERVICE_ADDR=productcatalogservice:3550
CURRENCY_SERVICE_ADDR=currencyservice:7000
CART_SERVICE_ADDR=cartservice:7070
RECOMMENDATION_SERVICE_ADDR=recommendationservice:8080
SHIPPING_SERVICE_ADDR=shippingservice:50051
CHECKOUT_SERVICE_ADDR=checkoutservice:5050
AD_SERVICE_ADDR=adservice:9555
Redis Cart

Image: redis:alpine
Port: 6379
