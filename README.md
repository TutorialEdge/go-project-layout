Go Project Layout
==================

This repository contains an example as to how I would typically structure my Go applications.

> Note - This is not a silver-bullet approach and flatter project structures may suit you if you are writing lightweight applications.

## Directory Overview

### cmd

This directory contains the entrypoints to our Go applications. The code in these files should be purely focused on the instantiation and the tearing down of our applications.

We can create subdirectories for each of the distinct types of entrypoints we require:

```output
- cmd/
  - server/
    - main.go
  - client/
    - main.go
  - cli/
    - main.go
```

### deploy

The `deploy` directory tends to contain files such as my kubernetes service and deployments. 

### internal

This directory should contain all of the internal implementation details that we do not wish to expose to other Go projects. 

I tend to the majority of my application code within an `internal` directory when I write HTTP or gRPC services as it's highly unlikely these packages will ever be imported and used by other Go projects.

Typically the internal directory ends up looking something like this:

```output
- internal/
-  clients/
-  - client.go
-  database/
-  - database.go
-  service/
-  - service.go
-  - service_test.go
-  transport/
-  - http/
-    - http.go
-  - grpc/
-    - grpc.go
``` 

### migrations

This directory contains all of the database migrations that my application will ultimately run against an underlying persistance layer. For example, if my app required a SQL-based database, this would contain all of the SQL migration files needed to create tables and alter columns etc.

### tests

This directory contains all of the E2E acceptance tests for our application. These tests should effectively treat our service as a black box and exercise all of the various API endpoints or equivalent for our applications.

```output
- tests/
  - api_test.go
```