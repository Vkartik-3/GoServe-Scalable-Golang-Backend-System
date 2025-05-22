# GoServe - Scalable Golang Backend System

A production-ready microservices architecture built with Go, featuring gRPC for inter-service communication and GraphQL as the API gateway. This project demonstrates modern backend development practices with a focus on scalability, maintainability, and performance.

## 🏗️ Architecture Overview

GoServe implements a distributed microservices architecture with the following components:

- **Account Service** - User account management and authentication
- **Catalog Service** - Product catalog and inventory management  
- **Order Service** - Order processing and management
- **GraphQL API Gateway** - Unified API interface for all services

## 🛠️ Technology Stack

- **Language**: Go (using stable older versions for production reliability)
- **Communication**: gRPC for inter-service communication
- **API Gateway**: GraphQL for client-facing API
- **Databases**: 
  - PostgreSQL (Account & Order services)
  - Elasticsearch (Catalog service)
- **Containerization**: Docker & Docker Compose
- **Protocol Buffers**: For gRPC service definitions

## 📁 Project Structure

```
GoServe/
├── account/          # Account microservice
├── catalog/          # Catalog microservice  
├── order/            # Order microservice
├── graphql/          # GraphQL API gateway
├── pb/               # Generated protobuf files
├── proto/            # Protocol buffer definitions
├── docker-compose.yml
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- Go 1.19+ (using stable version for production reliability)
- Docker & Docker Compose
- Protocol Buffers compiler

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Vkartik-3/GoServe-Scalable-Golang-Backend-System.git
cd GoServe-Scalable-Golang-Backend-System
```

2. **Set up Protocol Buffers**
```bash
# Download and install protoc
wget https://github.com/protocolbuffers/protobuf/releases/download/v23.0/protoc-23.0-linux-x86_64.zip
unzip protoc-23.0-linux-x86_64.zip -d protoc
sudo mv protoc/bin/protoc /usr/local/bin/

# Install Go plugins
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

# Update PATH
export PATH="$PATH:$(go env GOPATH)/bin"
source ~/.bashrc
```

3. **Generate gRPC files**
```bash
# Create pb directory
mkdir -p pb

# Generate protobuf files (example for account service)
protoc --go_out=./pb --go-grpc_out=./pb proto/account.proto
```

4. **Start the services**
```bash
docker-compose up -d --build
```

5. **Access GraphQL Playground**
Open your browser and navigate to: `http://localhost:8000/playground`

## 📚 API Usage

### Account Operations

**Query all accounts:**
```graphql
query {
  accounts {
    id
    name
  }
}
```

**Create a new account:**
```graphql
mutation {
  createAccount(account: {name: "John Doe"}) {
    id
    name
  }
}
```

### Product Operations

**Query products with pagination:**
```graphql
query {
  products(pagination: {skip: 0, take: 10}, query: "laptop") {
    id
    name
    description
    price
  }
}
```

**Create a product:**
```graphql
mutation {
  createProduct(product: {
    name: "Gaming Laptop"
    description: "High-performance gaming laptop"
    price: 1299.99
  }) {
    id
    name
    price
  }
}
```

### Order Operations

**Create an order:**
```graphql
mutation {
  createOrder(order: {
    accountId: "account_123"
    products: [{id: "product_456", quantity: 2}]
  }) {
    id
    totalPrice
    products {
      name
      quantity
    }
  }
}
```

**Query account with order history:**
```graphql
query {
  accounts(id: "account_123") {
    name
    orders {
      id
      createdAt
      totalPrice
      products {
        name
        quantity
        price
      }
    }
  }
}
```

## 🔧 Development

### Adding New Services

1. Create service directory with proper structure
2. Define gRPC service in `.proto` file
3. Generate Go code using protoc
4. Implement service logic
5. Update docker-compose.yml
6. Add GraphQL resolvers if needed

### Running Tests

```bash
# Run tests for all services
go test ./...

# Run tests for specific service
go test ./account/...
```

## 🐳 Docker Configuration

The project uses Docker Compose to orchestrate all services and their dependencies:

- **PostgreSQL** databases for Account and Order services
- **Elasticsearch** for Catalog service
- **Individual service containers** with proper networking

## 🛡️ Production Considerations

### Version Management Philosophy
This project uses stable, older versions of dependencies for production reliability. This approach provides:

- **Stability**: Proven versions with known behaviors
- **Maintainability**: Easier debugging and issue resolution
- **Risk Reduction**: Fewer surprises from breaking changes
- **Team Efficiency**: Especially important for small teams

### Security Features
- Input validation and sanitization
- gRPC authentication and authorization
- Database connection security
- Container security best practices

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built following microservices best practices
- Inspired by production-ready backend architectures
- Thanks to the Go community for excellent tooling

## 📞 Contact

**Kartik** - [@Vkartik-3](https://github.com/Vkartik-3)

Project Link: [https://github.com/Vkartik-3/GoServe-Scalable-Golang-Backend-System](https://github.com/Vkartik-3/GoServe-Scalable-Golang-Backend-System)
