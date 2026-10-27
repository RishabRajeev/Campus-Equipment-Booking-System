# Devops CIA2-23011102072
# Campus Equipment Booking Service
Java 17 / Spring Boot REST API for a CI/CD lab assessment.

## Assigned Change Request
**Positive Booking Quantity Validation**: Validates requested booking quantities to ensure only positive values are accepted[cite: 1, 2]. Zero and negative quantities are rejected without altering inventory or creating a confirmed booking[cite: 2].

## Defect Resolution
* **Defect Fixed**: Corrected a boundary condition where a booking was incorrectly accepted if the requested quantity was exactly one unit greater than available inventory[cite: 2].
* **Verification**: Added automated tests to verify that requests exactly equal to available inventory are accepted, and requests exceeding inventory, as well as zero and negative quantities, are rejected and do not modify the available inventory[cite: 2].

## Build and Test
* Run tests: `mvn clean test`
* Package application: `mvn clean package`[cite: 1]
* Run locally: `mvn spring-boot:run` — port 8080.

## Docker Instructions
* Build Image: `docker build -t campus-equipment-booking:set-e .`[cite: 2]
* Run Container: `docker run -d -p 8080:8080 --name equipment-booking campus-equipment-booking:set-e`[cite: 2]

## Kubernetes Deployment
* Start cluster & load image: `minikube start` && `minikube image load campus-equipment-booking:set-e`[cite: 2]
* Deploy resources: `kubectl apply -f deployment.yaml` and `kubectl apply -f service.yaml`[cite: 2]
* Scale replicas: `kubectl scale deployment equipment-booking-deployment --replicas=2`[cite: 2]

## Health Check Access Method
Due to Minikube network limitations on QEMU, the health endpoint is accessed via port forwarding[cite: 2]:
1. Run: `kubectl port-forward service/equipment-booking-service 8080:8080`
2. Access URL: `curl http://localhost:8080/actuator/health`[cite: 2]

## Endpoints
- `GET /api/equipment`
- `GET /api/equipment/{id}`
- `POST /api/bookings`
- `GET /api/bookings/{id}`
- `POST /api/bookings/{id}/cancel`
- `GET /actuator/health`

Inventory is in memory and resets on restart. No database is required.