# PetClinic Customers Service

## Overview
Manages pet owners and their pets. Part of the PetClinic multi-repo microservices demo.

## Tech Stack
- Java 17, Spring Boot 4.0.1, Spring Cloud 2025.1.0
- Spring Data JPA + HSQLDB (in-memory, default) or MySQL (`mysql` profile)
- Eureka client for service discovery
- Spring Cloud Config client

## Package Structure
```
org.springframework.samples.petclinic.customers
├── CustomersServiceApplication.java    # Main class
├── config/
│   └── MetricConfig.java               # Custom metrics
├── model/
│   ├── Owner.java                      # JPA entity
│   ├── Pet.java                        # JPA entity
│   ├── PetType.java                    # JPA entity
│   ├── OwnerRepository.java            # Spring Data repo
│   └── PetRepository.java             # Spring Data repo
└── web/
    ├── OwnerResource.java              # REST controller — /owners/**
    ├── PetResource.java                # REST controller — /owners/*/pets/**
    ├── OwnerRequest.java               # DTO
    ├── PetRequest.java                 # DTO
    ├── PetDetails.java                 # DTO
    ├── ResourceNotFoundException.java  # 404 exception
    └── mapper/
        ├── Mapper.java                 # Interface
        └── OwnerEntityMapper.java      # Owner mapping
```

## API Endpoints
- `GET /owners` — list all owners
- `GET /owners/{ownerId}` — get owner by ID
- `POST /owners` — create owner
- `PUT /owners/{ownerId}` — update owner
- `GET /petTypes` — list pet types
- `GET /owners/*/pets/{petId}` — get pet
- `POST /owners/{ownerId}/pets` — add pet to owner
- `PUT /owners/*/pets/{petId}` — update pet

## Build & Run
```bash
mvn clean package -DskipTests
# Runs on port 8081 (set by Config Server, random locally)
```

## Database
- Schema: `src/main/resources/db/hsqldb/schema.sql`
- Seed data: `src/main/resources/db/hsqldb/data.sql`
- Tables: `owners`, `pets`, `types`

## Service Registration
Registers as `customers-service` with Eureka. The API Gateway routes `/api/customer/**` to this service.
