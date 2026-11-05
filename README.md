# Campus Equipment Booking Service

A Java 17 and Spring Boot REST API for campus equipment booking.

## Technologies
- Java 17
- Spring Boot 3.3.5
- Maven
- JUnit 5
- Docker
- Kubernetes
- Minikube

## Build and Test

Run tests:
mvn clean test

Package application:
mvn clean package

## Run Locally

mvn spring-boot:run

Health check:
http://localhost:8080/actuator/health

## Docker

Build image:
docker build -t campus-equipment-booking:set-d .

Run container:
docker run -d --name campus-booking -p 8080:8080 campus-equipment-booking:set-d

Verify:
http://localhost:8080/actuator/health

## Kubernetes Deployment

Start Minikube:
minikube start --driver=docker

Load image:
minikube image load campus-equipment-booking:set-d

Deploy:
minikube kubectl -- apply -f deployment.yaml
minikube kubectl -- apply -f service.yaml

Check resources:
minikube kubectl -- get deployments
minikube kubectl -- get pods
minikube kubectl -- get services

Scale to two replicas:
minikube kubectl -- scale deployment campus-booking --replicas=2

Health check:
minikube kubectl -- port-forward service/campus-booking-service 8081:8080

Access:
http://localhost:8081/actuator/health

## Assigned Change Request – Set D

Implemented borrower identifier validation.

Missing, empty and whitespace-only borrower identifiers
are rejected.

Invalid borrower identifiers do not create confirmed
bookings or reduce available inventory.

Automated tests verify valid and invalid borrower identifiers.

## Booking Capacity Defect

Fixed the booking capacity validation condition.

Previously, the application allowed a booking quantity
one unit greater than available inventory.

The condition now rejects quantities exceeding available
inventory.

Tests verify exact-capacity bookings and over-capacity
rejections without modifying inventory.