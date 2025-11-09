# Frontend Service

The Frontend Service is the main entry point of the application — it serves the web user interface and communicates with backend services via gRPC.
It renders HTML templates, serves static assets, manages user sessions, and coordinates requests between Product Catalog, Cart, Payment, Shipping, and Recommendation services.
By default, it listens on port 8080.

## Building Locally

The Frontend Service requires Go 1.23 (or higher).
To install dependencies, run:
```sh
go mod download
```

To build and run the Frontend Service:
```sh
go build -o frontend.exe
.\frontend.exe
```

If you see errors about missing environment variables, set these before running.
```sh
$env:PRODUCT_CATALOG_SERVICE_ADDR="localhost:3550"
$env:CART_SERVICE_ADDR="localhost:7070"
$env:CURRENCY_SERVICE_ADDR="localhost:7000"
$env:PAYMENT_SERVICE_ADDR="localhost:50051"
$env:SHIPPING_SERVICE_ADDR="localhost:50052"
$env:RECOMMENDATION_SERVICE_ADDR="localhost:8080"
$env:CHECKOUT_SERVICE_ADDR="localhost:5050"
$env:AD_SERVICE_ADDR="localhost:9555"
$env:SHOPPING_ASSISTANT_SERVICE_ADDR="localhost:6060"
```

Then open your browser at: http://localhost:8080

Expected Output
```sh
{"message":"Tracing disabled.","severity":"info"}
{"message":"Profiling disabled.","severity":"info"}
{"message":"Starting frontend service on port 8080","severity":"info"}
```

## Unit Testing

Basic unit tests are available for money and validation logic.
These ensure correct currency handling and input validation.
```sh
go test .
```

Expected Output
```sh
ok      frontend/money       0.002s
ok      frontend/validator   0.001s
```

## Building Docker

From this Frontend Service folder, run:
```sh
docker build -t frontend:latest .
```

Then start the container:
```sh
docker run -p 5050:5050 frontend:latest
```