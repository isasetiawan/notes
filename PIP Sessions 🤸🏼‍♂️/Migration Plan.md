## Topology Design
![[Pasted image 20240719132606.png]]

## Reasons
### AWS Elastic Container Service (ECS)
AWS ECS is choosen due to it compatible with Service Oriented Architecture. ECS has the following features:
1. **Fully Managed**: ECS is a fully managed service hence it suitable for small team. Since it manage the underlying infrastructure.
 2. **Auto Scaling**: ECS provides auto scaling for services. You can define the minimum and maximum number of tasks for a service.
 3. **Service Discovery**: ECS provides service discovery for services. You can use service discovery to route traffic to the correct service.
### Communication between services
To enable communication between services, Service Discovery is used. Service Discovery is a mechanism to discover services in a network. Service Discovery is used to route traffic to the correct service.
To ensure security, the communications between services are encrypted using TLS/SSL. The certificates are managed by AWS Certificate Manager.
### Database
Based on RCA there is no issue with database connection. Hence, The database be shared among the services.
