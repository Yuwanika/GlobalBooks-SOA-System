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

## 🖇️Architecture Overview

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
  
   ### 📌Integration Architecture

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

