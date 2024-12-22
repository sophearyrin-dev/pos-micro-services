![image](https://github.com/user-attachments/assets/6b7e487e-d80b-4213-8dde-86acda6f6fae)

![image](https://github.com/user-attachments/assets/b74b9db9-303c-4221-98e1-6f8ae3c85652)

@Transactional

The @Transactional annotation in the OrderService class is used to manage database transactions declaratively in a Spring application. If a method in the OrderService performs multiple database operations (e.g., creating an order, updating inventory, and recording a payment), @Transactional ensures that these operations are treated as a single transaction. If any operation fails, all changes are rolled back.


@LoadBalanced:

This annotation adds load-balancing capabilities to the WebClient.Builder. It allows the WebClient to resolve service names (e.g., inventory-service) into multiple instances and distribute the requests across them.

**1. Load Balancer**
Purpose:
A Load Balancer is a component that distributes incoming requests across multiple instances of a service to achieve better scalability, reliability, and performance.

Key Features:
Distributes Traffic: Ensures no single instance becomes a bottleneck.
Health Checks: Monitors the health of instances and routes traffic only to healthy ones.
Fault Tolerance: Automatically redirects traffic away from failed instances.
Algorithms: Uses techniques like Round Robin, Least Connections, or Random to distribute traffic.
Example:
Imagine you have 3 instances of an Inventory Service:

http://192.168.1.1:8080
http://192.168.1.2:8080
http://192.168.1.3:8080
A Load Balancer (e.g., Nginx, AWS Elastic Load Balancer) routes requests like this:

Request 1 → 192.168.1.1
Request 2 → 192.168.1.2
Request 3 → 192.168.1.3

**2. Eureka (Service Discovery)**
Purpose:
Eureka is a service discovery tool that helps microservices find and communicate with each other dynamically without hardcoding service locations (IP/Port).

Key Features:
Service Registry: Keeps track of all available service instances.
Dynamic Discovery: Microservices can discover each other by querying Eureka using their service names.
Client-Side Load Balancing: When multiple instances of a service are registered, Eureka provides a list of instances, allowing clients (like Ribbon or WebClient) to implement load balancing.
How It Works:
Service Registration:
Each service registers itself with Eureka.
Example: Inventory Service registers as inventory-service with Eureka.
Service Discovery:
Other services (like Order Service) query Eureka to find the instances of inventory-service.
Example:
Registered Instances in Eureka:
inventory-service → [192.168.1.1:8080, 192.168.1.2:8080, 192.168.1.3:8080]
Order Service queries Eureka for inventory-service and gets the list of instances.

**3. API Gateway**
Purpose:
An API Gateway acts as a single entry point for all client requests in a microservices architecture, handling routing, security, rate limiting, and other cross-cutting concerns.

Key Features:
Routing: Forwards client requests to the appropriate microservices.
Centralized Security: Enforces authentication and authorization policies.
Request Transformation: Modifies requests or responses (e.g., aggregating data from multiple services).
Rate Limiting: Limits the number of requests to protect backend services.
Protocol Translation: Converts protocols (e.g., HTTP to gRPC).
Example:
If a client wants to:

Place an order → /order-service/orders
Check inventory → /inventory-service/products
The API Gateway routes these requests:

/order-service/orders → Order Service
/inventory-service/products → Inventory Service
Popular Tools:
Spring Cloud Gateway
Kong
Nginx
AWS API Gateway
How They Work Together
In a microservices architecture, these components complement each other:

**Eureka (Service Discovery):**

Keeps track of available service instances dynamically.
Example: Order Service queries Eureka to find instances of Inventory Service.
Load Balancer:

Distributes traffic among multiple instances of a service discovered through Eureka.
Can be implemented on the client-side (via Ribbon, WebClient) or server-side (e.g., AWS ELB).

**API Gateway:**

Serves as the single entry point for clients.
Uses Eureka to discover services and may delegate request routing and load balancing.
Comparison Table
Feature	Load Balancer	Eureka	API Gateway
Purpose	Distributes requests across instances.	Provides service discovery.	Acts as a single entry point for clients.
Service Awareness	Works with registered instances.	Tracks and provides service instance details.	Uses Eureka or static routing for services.
Traffic Distribution	Yes	No	Yes (indirectly through routing).
Security	No	No	Yes (e.g., authentication, rate limiting).
Request Transformation	No	No	Yes
Tools	Nginx, HAProxy, AWS ELB, Ribbon	Netflix Eureka, Consul	Spring Cloud Gateway, Kong, Nginx
Example Use Case
Without These Components:
Client directly calls http://192.168.1.1:8080 for inventory-service.
If the IP changes or the instance crashes, the client can't recover.
With Eureka + Load Balancer + API Gateway:
Eureka: Registers inventory-service and provides a list of available instances.
Load Balancer: Distributes requests to available instances.
API Gateway: Client calls a single entry point (e.g., http://api.mysite.com/inventory) instead of individual instances.





