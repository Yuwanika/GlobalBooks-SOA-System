# 📚GlobalBooks SOA System📖

GlobalBooks Inc. is struggling with a big, old-fashioned system that is hard to change and slows down during peak demand. Every time they change a single feature, they have to redeploy the whole system, which increases risk and downtime. To solve this, I redesigned the system using Service-Oriented Architecture (SOA). I broke it into four separate services: Catalog, Orders, Payments, and Shipping. Each service has its own job, can run on its own, and communicates with others through standard technologies like SOAP, REST, BPEL, and RabbitMQ. I also added security with WS-Security for SOAP and OAuth2 for REST.

## ⚙️System Highlights

- **Hybrid Architecture**: Seamless integration of SOAP and REST services
- **Enterprise Integration**: Message-driven architecture with RabbitMQ
- **Security**: Comprehensive security implementation with OAuth2 and WS-Security
- **Scalability**: Containerized microservices with Docker and Kubernetes support
- **Monitoring**: Built-in health checks and metrics collection
- **Documentation**: Complete API documentation and architectural diagrams
- **Testing**: Comprehensive test suites for all services 

## 🪩Architecture Overview

### 📌Core Services Architecture

1. **Catalog Service (SOAP)** - Port 8081
   - Technology: Java Spring Boot with JAX-WS
   - Protocol: SOAP with WS-Security
   - Features:
     * Comprehensive book catalog management
     * Real-time pricing and availability checks
     * Category and search functionality
     * Inventory synchronization
   - Integration: Exposes WSDL for service discovery

2. **Orders Service (REST)** - Port 8088
    - Technology: Java Spring Boot
    - Protocol: REST with OAuth2
    - Features:
      * Order lifecycle management
      * Order tracking and history
      * Business process orchestration
      * Event-driven updates
    - Integration: Publishes events to RabbitMQ

3. **Payments Service (REST)** - Port 8083
    - Technology: Java Spring Boot
    - Protocol: REST microservice
    - Features:
      * Secure payment processing
      * Multiple payment method support
      * Transaction history
      * Refund processing
    - Security: PCI-DSS compliance ready

4. **Shipping Service (REST)** - Port 8084
    - Technology: Java Spring Boot
    - Protocol: REST microservice
    - Features:
      * Shipment tracking
      * Delivery estimation
      * Multi-carrier support
      * Address validation
    - Integration: Real-time shipping updates
  
###  📌Integration Architecture

1. **Message Broker (RabbitMQ)**
   - Enterprise Service Bus (ESB) implementation
   - Asynchronous message patterns
   - Dead letter queues for error handling
   - Message persistence and reliability

2. **Process Orchestration (BPEL)**
   - Order fulfillment workflow orchestration
   - Long-running transaction management
   - Error compensation handling
   - Business process monitoring

3. **Security Framework**
   - OAuth2 authentication for REST services
   - WS-Security for SOAP services
   - JWT token management
   - Role-based access control (RBAC)

## 🖥️System Requirements

### Development Environment
- Java Development Kit (JDK) 17 or higher
- Maven 3.9.11
- Docker Engine 20.10+
- Docker Compose 2.0+
- Git 2.0+
- 8GB RAM minimum (16GB recommended)
- 20GB free disk space

### Production Environment
- Kubernetes 1.20+ cluster
- Node requirements:
  * 16GB RAM minimum per node
  * 4 CPU cores minimum per node
  * 50GB storage per node
- Load Balancer support
- Persistent Volume support

## ♨️Quick Start Guide

1. **Clone and Setup**
   ```bash
   # Clone the repository
   git clone <repository-url>
   cd SOA

   # Setup environment variables
   copy .env.example .env
   # Edit .env with your configurations
   ```

2. **Build and Deploy**
   ```bash
   # Build all services
   ./13-scripts/build-all-services.sh

   # Deploy using Docker Compose
   cd 10-deployment
   docker compose up -d --build
   ```

3. **Verify System Health**
   ```bash
   # Run health check script
   ./13-scripts/verify-deployment.sh
   ```

   Or check individual endpoints:
   - Catalog Service: http://localhost:8081/soap/catalog?wsdl
   - Orders API: http://localhost:8088/api/v1/orders/health
   - Payments API: http://localhost:8083/api/v1/payments/health
   - Shipping API: http://localhost:8084/api/v1/shippings/health
   - RabbitMQ Dashboard: http://localhost:15672 
     

4. **Access Documentation**
   - API Documentation: http://localhost:8082/swagger-ui.html
   - Architecture Diagrams: `01-design-artifacts/architecture-diagrams/`
   - Integration Guide: `11-documentation/integration-guide.md`

  ## ⏺️Service Endpoints

### Orders Service (REST API)

```
POST   /api/v1/orders                    # Create new order
GET    /api/v1/orders                    # Get all orders
GET    /api/v1/orders/{id}               # Get order by ID
PUT    /api/v1/orders/{id}/status        # Update order status
DELETE /api/v1/orders/{id}               # Cancel order
GET    /api/v1/orders/health             # Health check
```

### Payments Service (REST API)

```
POST   /api/v1/payments/initiate         # Initiate payment
POST   /api/v1/payments/{id}/process     # Process payment
GET    /api/v1/payments/{id}             # Get payment details
GET    /api/v1/payments/order/{orderId}  # Get payments by order
GET    /api/v1/payments/health           # Health check
```

### Shipping Service (REST API)

```
POST   /api/v1/shippings                 # Create shipping
POST   /api/v1/shippings/{id}/process    # Process shipping
GET    /api/v1/shippings/{id}            # Get shipping details
GET    /api/v1/shippings/tracking/{num}  # Track shipment
GET    /api/v1/shippings/health          # Health check
```

### Catalog Service (SOAP)

WSDL available at: http://localhost:8081/soap/catalog?wsdl

Operations:
- `searchBooks` - Search books by query and category
- `getBookById` - Get book details by ID
- `getBookPrice` - Get book price
- `checkAvailability` - Check book availability

## 📩Message Flow

1. **Order Creation**: Client places order via Orders Service REST API
2. **Event Publishing**: Orders Service publishes events to RabbitMQ
3. **Payment Processing**: Payments Service consumes payment events
4. **Shipping Processing**: Shipping Service consumes shipping events
5. **Orchestration**: BPEL process coordinates the entire workflow

## 🔐Security

### Current Implementation
- **SOAP Services**: Basic authentication (WS-Security can be added later)
- **REST Services**: OAuth2 JWT token-based authentication (configuration provided)
- **Keycloak**: Integrated for identity management (available in Docker setup)

### Planned Security Features
- WS-Security with UsernameToken authentication for SOAP services
- Complete OAuth2 implementation for REST services
- Mutual TLS authentication between services

## ❓Testing

### Postman Collections
- `09-testing/postman/GlobalBooks-SOA-Catalog.postman_collection.json`
- `09-testing/postman/GlobalBooks_Orders_API.postman_collection.json`

### SOAP UI Tests
- `09-testing/soap-ui/CatalogService-TestSuite.xml`

## 🔀Development

### Setting Up Development Environment

1. **Install Required Tools**
   ```bash
   # Verify Java 17+ installation
   java -version
   
   # Verify Maven 3.9+
   mvn -version
   
   # Verify Docker
   docker --version
   docker-compose --version
   ```

2. **Configure Environment**
   ```bash
   # Set up development environment
   cd 13-scripts
   ./setup-environment.sh
   ```

### Building Individual Services

```bash
# Catalog Service
cd 02-catalog-service
mvn clean package

# Orders Service
cd 03-orders-service
mvn clean package

# Payments Service
cd 04-payments-service
mvn clean package

# Shipping Service
cd 05-shipping-service
mvn clean package
```

### Running Services Locally
   ```bash
   # Catalog Service (Port 8081)
   cd 02-catalog-service
   mvn spring-boot:run

   # Orders Service (Port 8088)
   cd 03-orders-service
   mvn spring-boot:run

   # Payments Service (Port 8083)
   cd 04-payments-service
   mvn spring-boot:run

   # Shipping Service (Port 8084)
   cd 05-shipping-service
   mvn spring-boot:run
   ```

3. **Verify Services**
   ```bash
   # Check health endpoints
   curl http://localhost:8081/soap/catalog?wsdl
   curl http://localhost:8088/api/v1/orders/health
   curl http://localhost:8083/api/v1/payments/health
   curl http://localhost:8084/api/v1/shippings/health
   ```

### Development Best Practices

1. **Code Quality**
   - Run static code analysis:
     ```bash
     mvn sonar:sonar
     ```
   - Format code before commit:
     ```bash
     mvn formatter:format
     ```

2. **Testing**
   - Run unit tests:
     ```bash
     mvn test
     ```
   - Run integration tests:
     ```bash
     mvn verify
     ```
   - Load test scripts available in `09-testing/performance/`

3. **Documentation**
   - Update API documentation in `11-documentation/api-docs/`
   - Generate updated API docs:
     ```bash
     mvn javadoc:javadoc
     ```

## 📈Monitoring

- Health checks available on all services
- RabbitMQ management interface for message monitoring
- Spring Boot Actuator endpoints for metrics

## 🔄Deployment

### Docker Deployment
```bash
cd 10-deployment
docker compose up -d --build
```

### Kubernetes Deployment
Kubernetes manifests available in `10-deployment/kubernetes/`

## 🧮Architecture Patterns Demonstrated

- **Service-Oriented Architecture (SOA)**
- **Enterprise Service Bus (ESB)**
- **Event-Driven Architecture**
- **Microservices**
- **API Gateway Pattern**
- **Circuit Breaker Pattern**
- **Saga Pattern** (via BPEL orchestration)

## 🛠️Technologies Used

- **Java 17** - Primary programming language
- **Spring Boot** - Application framework
- **Spring Web Services** - SOAP implementation
- **RabbitMQ** - Message broker
- **Docker** - Containerization
- **OAuth2** - REST API security
- **WS-Security** - SOAP security
- **BPEL** - Business process orchestration
- **H2 Database** - In-memory database for development

## ✏️Project Structure

# Project Structure

<details>
<summary>01-design-artifacts/ – Architecture and Design Documentation</summary>

- `architecture-diagrams/` – System architecture visuals  
- `governance-policy.md` – SOA governance guidelines  
- `soa-design-document.md` – Detailed design specifications  

</details>

<details>
<summary>02-catalog-service/ – SOAP-based Catalog Service</summary>

- `src/` – Service source code  
- `Dockerfile` – Container configuration  
- `pom.xml` – Maven configuration  

</details>

<details>
<summary>03-orders-service/ – REST-based Orders Service</summary>

- `src/` – Service implementation  
- `Dockerfile` – Container configuration  
- `pom.xml` – Maven build config  

</details>

<details>
<summary>04-payments-service/ – Payment Processing Service</summary>

- `src/` – Service implementation  
- `Dockerfile` – Container configuration  
- `pom.xml` – Maven build config  

</details>

<details>
<summary>05-shipping-service/ – Shipping Management Service</summary>

- `src/` – Service implementation  
- `Dockerfile` – Container configuration  
- `pom.xml` – Maven build config  

</details>

<details>
<summary>06-bpel-orchestration/ – Business Process Orchestration</summary>

- `deployment/` – BPEL deployment configs  
- `processes/` – BPEL process definitions  
- `wsdl/` – Service WSDL files  

</details>

<details>
<summary>07-integration/ – Integration Components</summary>

- `consumers/` – Message consumers  
- `producers/` – Event producers  
- `rabbitmq/` – Message broker configs  

</details>

<details>
<summary>08-security/ – Security Configurations</summary>

- `certificates/` – SSL/TLS certificates  
- `oauth2/` – OAuth2 configurations  
- `ws-security/` – WS-Security settings  

</details>

<details>
<summary>09-testing/ – Testing Resources</summary>

- `integration-tests/` – Integration test suites  
- `performance/` – Performance test scripts  
- `postman/` – API test collections  
- `soap-ui/` – SOAP service tests  

</details>

<details>
<summary>10-deployment/ – Deployment Configurations</summary>

- `docker-compose.yml` – Local deployment  
- `kubernetes/` – K8s manifests  
- `cloud/` – Cloud-specific configs  
- `scripts/` – Deployment automation  

</details>

<details>
<summary>11-documentation/ – System Documentation</summary>

- `api-docs/` – API specifications  

</details>

<details>
<summary>12-reports/ – Project Reports</summary>

- `viva-presentation/` – Project presentations  

</details>

<details>
<summary>13-scripts/ – Utility Scripts</summary>

- `setup-environment.sh` – Environment setup  
- `test-soa-workflow.sh` – Workflow testing  

</details>


Each directory contains a dedicated README with specific setup instructions and additional details.


