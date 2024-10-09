# CQRS API in Domain-Centric Design Architecture

This project demonstrates the implementation of a CQRS API in a domain-centric design architecture using .NET 8 and Mediator with request pipeline.

## Features

- **CQRS Implementation**: Separation of concerns between read and write operations.
- **Domain-Centric Design**: Focus on the domain model and business logic.
- **Mediator with Request Pipeline**: Utilizes Mediator pattern for handling requests and responses with a configurable pipeline.

## Benefits of Request Pipeline with Mediator

### Simplified Request Handling
The request pipeline simplifies the handling of requests by providing a unified entry point for processing.

### Centralized Middleware Dependencies
Using Mediator as a middleware dependency centralizes the handling of cross-cutting concerns such as logging, validation, and authorization, reducing code duplication.

### Improved Testability
The request pipeline and Mediator pattern enhance testability by allowing easy isolation of components for unit testing.
