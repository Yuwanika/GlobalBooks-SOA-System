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
