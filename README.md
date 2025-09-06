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
