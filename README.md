

# 🚗 Automotive Financing Platform

### Enterprise Web Application for Automotive Financing & Leasing

A cloud-deployed web application developed with Spring Boot 3 that automates automotive financing quotations, leasing calculations, business rule management, and secure PDF proposal generation.

---

### 🌐 Live Demo

> **Demo Environment**
>
> This application is deployed on Railway for demonstration purposes.
> Some administrative features require authentication.

> https://cotizador-production-0680.up.railway.app/creditos/automotriz/simulador

---

![Architecture](images/architecture-overview.png)

---

![Java](https://img.shields.io/badge/Java-17-orange?style=for-the-badge)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.3-6DB33F?style=for-the-badge)
![Spring Security](https://img.shields.io/badge/Spring_Security-6-6DB33F?style=for-the-badge)
![JWT](https://img.shields.io/badge/JWT-Authentication-blue?style=for-the-badge)
![Hibernate](https://img.shields.io/badge/Hibernate-JPA-59666C?style=for-the-badge)
![MySQL](https://img.shields.io/badge/MySQL-8-4479A1?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge)
![Railway](https://img.shields.io/badge/Railway-Cloud-black?style=for-the-badge)
![JasperReports](https://img.shields.io/badge/JasperReports-PDF-red?style=for-the-badge)



## 📌 Business Problem

Automotive financing requires accurate and flexible calculations that can adapt to different financial products, vehicle conditions, interest rates, and business rules.

Traditional quotation processes can involve manual calculations and multiple sources of information, making the process time-consuming and increasing the risk of inconsistencies.

The **Automotive Financing Platform** was designed to provide a centralized solution for generating automotive financing and leasing quotations while allowing business users to manage the rules and parameters that control the calculation process.

### Business objectives

- Automate automotive financing calculations.
- Support different financing and leasing scenarios.
- Generate detailed amortization schedules.
- Centralize interest rate management.
- Configure business rules without modifying application code.
- Generate professional PDF quotation documents.
- Provide secure access to administrative functionality.
- Maintain a clear separation between business logic, persistence, security, and presentation.

## 💡 Solution Overview

The **Automotive Financing Platform** provides a centralized web application for simulating and managing automotive financing products.

The platform combines financial calculation services, business rules, administration capabilities, security, and document generation into a single application.

### Core Capabilities

#### 🚗 Credit & Leasing Simulation

The platform supports different automotive financing scenarios, including:

- Fixed-rate financing.
- Variable-rate financing.
- Leasing with residual value.
- Down payment configuration.
- Financing term selection.
- Vehicle and model selection.
- Payment calculation.
- Detailed amortization schedules.

#### 📊 Financial Calculation

The calculation engine processes the quotation parameters and generates the corresponding payment schedule, including:

- Principal balance.
- Interest.
- Capital repayment.
- Charges.
- Payment dates.
- Remaining balance.

#### ⚙️ Business Rules Management

The platform provides configurable business rules that allow administrators to control parameters used during the automotive financing process.

##### Payment Due Day

Administrators can define the payment due day used to generate the amortization schedule.

For example, if the configured payment day is **15**, the generated amortization schedule will use the 15th day of each corresponding payment period as the due date.

This allows the platform to support different business policies, such as payment schedules with due dates on the 1st, 15th, or another configured day of the month.

##### Used Vehicle Eligibility

The platform allows administrators to configure the maximum vehicle age accepted for automotive financing.

This rule is particularly relevant for used vehicles, where financing institutions may establish an age limit as part of their credit policies.

For example, if the configured maximum vehicle age is **8 years**, vehicles exceeding the applicable age policy are not considered eligible for financing.

##### Automatic Processes

The platform provides a configurable list of processes that can be executed by the system.

Currently, the implemented process is related to **Residual Value** for pure leasing.

In a pure leasing scenario, the residual value represents the amount that remains outstanding at the end of the financing term.

For example, for a vehicle valued at **$1,000,000** with a residual value of **$400,000**, the amortization schedule is structured so that the final outstanding balance is $400,000.

At the end of the lease, the customer has the right to purchase the vehicle for the configured residual value.

#### 📄 PDF Quotation Generation

The platform generates professional PDF documents containing the quotation information and payment schedule using **JasperReports**.

Report access is protected through a dedicated JWT-based mechanism.

#### 🔐 Security & Administration

Administrative functionality is protected using **Spring Security**, with authentication and role-based authorization.

The application also exposes REST endpoints secured through JWT authentication for specific services.

#### 🌐 External Integration

The application integrates with **BANXICO** services through Spring WebClient to retrieve financial information used by the platform.

#### 📈 Variable Rate Calculation

For variable-rate financing, the platform retrieves the applicable reference rate from **BANXICO** and combines it with a configurable financial margin.

The calculation follows the business rule:

**Base Rate = BANXICO Reference Rate + Financial Margin**

The resulting base rate is then used by the calculation engine to generate the corresponding amortization schedule.

The financial margin is configurable through the administration module, allowing the business user to adjust the spread applied to the reference rate without modifying the application source code.

## 🏗️ Architecture

The **Automotive Financing Platform** follows a layered architecture designed to separate presentation, business logic, security, and data persistence responsibilities.

The application is built as a **Spring Boot 3 monolithic web application**, using Thymeleaf for the web interface and exposing selected REST endpoints for API-based operations.

### Architecture Overview

![Architecture Overview](images/architecture-overview.png)

The main components of the solution are:

- **Presentation Layer** — Thymeleaf, HTML, CSS and Bootstrap provide the web interface.
- **Controller Layer** — Spring MVC controllers handle HTTP requests and coordinate application flows.
- **Business Layer** — Facades and services encapsulate financial calculations, business rules, leads, rates, and report generation.
- **Persistence Layer** — Spring Data JPA and Hibernate provide ORM capabilities for interacting with MySQL.
- **Security Layer** — Spring Security provides authentication and authorization, while JWT is used for selected REST services and protected report operations.
- **Reporting** — JasperReports generates PDF quotation documents.
- **External Integration** — Spring WebClient is used to retrieve reference rate information from BANXICO.
- **Database** — MySQL stores quotations, vehicles, rates, business rules, users, and related application data.

## 🛠️ Technology Stack

### Backend

| Technology | Purpose |
|---|---|
| **Java 17** | Application development language |
| **Spring Boot 3.3** | Application framework |
| **Spring MVC** | Web and REST request handling |
| **Spring Data JPA** | Data access and persistence |
| **Hibernate** | ORM and entity management |
| **Maven** | Dependency management and build automation |

### Frontend

| Technology | Purpose |
|---|---|
| **Thymeleaf** | Server-side HTML rendering |
| **Bootstrap 5** | Responsive user interface |
| **HTML5 / CSS3** | Web presentation |

### Database

| Technology | Purpose |
|---|---|
| **MySQL 8** | Relational database |
| **JPA / Hibernate** | Object-relational mapping |

### Security

| Technology | Purpose |
|---|---|
| **Spring Security** | Authentication and authorization |
| **JWT** | Stateless authentication for selected REST services and protected report operations |

### Reporting

| Technology | Purpose |
|---|---|
| **JasperReports** | PDF quotation generation |

### External Integration

| Technology | Purpose |
|---|---|
| **Spring WebClient** | HTTP client for external API integration |
| **BANXICO API** | Reference rate information used in variable-rate calculations |

### DevOps & Deployment

| Technology | Purpose |
|---|---|
| **Docker** | Application containerization |
| **Docker Compose** | Local multi-container development environment |
| **Docker Hub** | Container image registry |
| **Railway** | Cloud deployment and hosting |
| **Git** | Version control |

### API Documentation

Selected REST endpoints are documented using **OpenAPI / Swagger**, providing an interactive interface for exploring and testing the application's APIs.

## ✨ Key Features

### 🚗 Automotive Financing Simulation

- Automotive credit quotation generation.
- New and used vehicle financing.
- Vehicle brand, model, and year selection.
- Configurable financing terms.
- Down payment configuration.
- Fixed-rate financing.
- Variable-rate financing.
- Pure leasing with residual value.
- Detailed amortization schedules.

### 📊 Financial Calculation Engine

- Automated payment calculation.
- Interest and principal breakdown.
- Payment schedule generation.
- Configurable payment due dates.
- Residual balance calculation for leasing scenarios.
- Support for configurable financial margins.

### ⚙️ Business Rules Administration

Administrators can configure key parameters that control the quotation process:

- Payment due day.
- Maximum vehicle age for financing.
- Financial margin for variable-rate products.
- Automatic processes.
- Residual value configuration.

### 📈 Variable Rate Integration

- Reference rate retrieval through BANXICO integration.
- Configurable financial margin.
- Dynamic base-rate calculation.
- Integration of external financial data into the quotation engine.

### 📄 PDF Reports

- Professional quotation document generation.
- Amortization schedule included in generated reports.
- JasperReports integration.
- Protected report access using JWT-based tokens.

### 🔐 Authentication & Authorization

- Spring Security integration.
- Secure administrative area.
- Role-based authorization.
- Session-based authentication for web administration.
- JWT authentication for selected REST services.
- JWT-protected report access.

### 🌐 REST API

- REST endpoints for selected application services.
- OpenAPI / Swagger documentation.
- Interactive API exploration and testing.

### 🐳 Containerized Deployment

- Dockerized Spring Boot application.
- Docker Compose environment for local development.
- MySQL container for local persistence.
- Docker Hub image management.
- Cloud deployment through Railway.

## 📸 Screenshots

### 🔐 Authentication

Secure access to the administration area using Spring Security.

![Login](images/login.png)

---

### 🚗 Automotive Financing Simulation

The main quotation interface allows users to configure the vehicle, financing parameters, and product conditions to generate an automotive financing proposal.

![Automotive Financing Simulation](images/simulador.png)

---

### 📊 Amortization Schedule

The platform generates a detailed amortization schedule based on the selected financing conditions, including payment dates, principal, interest, charges, and outstanding balance.

![Amortization Schedule](images/amortization-tabl.png)

---

### ⚙️ Business Rules Administration

Authorized administrators can configure the parameters that control the quotation process, including payment due dates, vehicle eligibility rules, and automatic processes.

![Business Rules](images/business-rules.png)

---

### 📈 Interest Rate Management

The administration module allows authorized users to manage the interest-rate parameters used by the financial calculation engine, including the configurable financial margin used in variable-rate calculations.

![Interest Rate Management](images/rates-management.png)

---

### 📄 PDF Quotation

The generated quotation can be exported as a professional PDF document containing the financing information and amortization schedule.

![PDF Quotation](images/amortization-table_PDF.png)

## 🔒 Security Architecture

The platform implements multiple security mechanisms depending on the type of resource being accessed.

### Web Application Security

The administrative web application uses **Spring Security** for authentication and authorization.

The administration area is protected through role-based access control, ensuring that only authorized users can access configuration and management functionality.

```text
User
  │
  ▼
Spring Security
  │
  ├── Authentication
  │
  └── Role-based Authorization
          │
          ▼
    Administration
```

### JWT Authentication

Selected REST services use **JWT-based authentication** to support stateless API access.

```text
Client
  │
  │ Login credentials
  ▼
Authentication Endpoint
  │
  ▼
JWT Token
  │
  ▼
Protected REST Endpoint
  │
  ▼
JWT Validation
  │
  ▼
Authorized Request
```

### Protected PDF Reports

PDF report generation uses a dedicated JWT-based token mechanism.

The application generates a short-lived token associated with the requested quotation, which is then used to securely access the generated report.

```text
Quotation Request
       │
       ▼
Generate Report Token
       │
       ▼
Short-lived JWT
       │
       ▼
Protected PDF Endpoint
       │
       ▼
JasperReports
       │
       ▼
PDF Document
```

### Security Principles

The security implementation follows these principles:

- Role-based authorization for administrative functionality.
- Stateless JWT authentication for selected REST services.
- Short-lived tokens for protected report access.
- Secrets provided through environment variables.
- Separation between authentication, authorization, and business logic.

## 🚀 Deployment

The application is fully containerized using Docker and deployed to the cloud using Railway.

The deployment architecture consists of:

- Spring Boot application packaged as a Docker image.
- Docker Hub as the container registry.
- Railway as the cloud hosting platform.
- MySQL as the relational database.
- Environment variables for secure configuration management.

### Deployment Workflow

```text
Developer
     │
     ▼
 Maven Build
     │
     ▼
 Docker Image
     │
     ▼
 Docker Hub
     │
     ▼
 Railway Deployment
     │
     ▼
 Production Environment
```

### Environment Variables

The application uses environment variables for sensitive configuration.

| Variable | Description |
|-----------|-------------|
| DB_URL | Database connection URL |
| DB_USER | Database username |
| DB_PASSWORD | Database password |
| JWT_SECRET | JWT signing secret |
| REPORT_JWT_SECRET | Report JWT signing secret |

> Sensitive values are intentionally omitted from this repository.

### Deployment Highlights

- ✅ Dockerized Spring Boot application
- ✅ Cloud deployment on Railway
- ✅ Environment-based configuration
- ✅ Container image versioning
- ✅ Separate development and production environments

### Live Demo

The latest deployed version is available at:

https://cotizador-production-0680.up.railway.app/creditos/automotriz/simulador

### Containerization

The application runs inside a Docker container, ensuring a consistent execution environment across local development and cloud deployment.

Containerization also simplifies versioning, portability, and deployment automation.

## 🌐 API Documentation

The **Automotive Financing Platform** exposes REST endpoints for selected application services.

The API is documented using **OpenAPI / Swagger**, providing an interactive interface for exploring endpoints, reviewing request and response schemas, and testing API operations.

### API Modules

| Module | Description |
|---|---|
| **Authentication** | User authentication and JWT token generation |
| **Rates** | Interest-rate management and retrieval |
| **Automotive Financing** | Services related to automotive credit quotations |
| **Vehicles** | Vehicle brands, models, and related information |
| **Leads** | Lead and quotation-related operations |
| **Reports** | Secure report-token generation and PDF report access |

### API Capabilities

- RESTful HTTP endpoints.
- OpenAPI-based documentation.
- Interactive Swagger UI.
- Request parameter documentation.
- Response schema documentation.
- JWT authentication for selected protected endpoints.
- HTTP status and error response documentation.

### Swagger UI

When running the application locally, the API documentation is available through Swagger UI:

```text
http://localhost:8080/swagger-ui/index.html
```

The Swagger interface allows developers to inspect and test the available API operations directly from the browser.

> **Note:** API documentation and endpoint availability may vary between development and production environments.

## 🐳 Deployment & Infrastructure

The application is containerized using **Docker** and deployed to the cloud through **Railway**.

### Deployment Architecture

```text
Developer Workstation
        │
        │ Maven Build
        ▼
   Spring Boot JAR
        │
        │ Docker Build
        ▼
   Docker Image
        │
        │ Push
        ▼
     Docker Hub
        │
        │ Deploy
        ▼
      Railway
        │
        ├───────────────┐
        ▼               ▼
 Spring Boot       MySQL Database
 Application
        │
        ▼
     BANXICO
   External API
```

### Containerization

The application is packaged as a Docker image containing the Spring Boot application and its runtime environment.

The containerized approach provides:

- Consistent application runtime.
- Reproducible deployments.
- Environment-based configuration.
- Separation between application and infrastructure.
- Simplified deployment across environments.

### Local Development Environment

Docker Compose is used to run the application and MySQL database locally.

```text
Docker Compose
      │
      ├── Spring Boot Application
      │        │
      │        ▼
      │     MySQL
      │
      └── Network
```

Database credentials and application configuration are provided through environment variables rather than hard-coded application properties.

### Cloud Deployment

The application is deployed to **Railway** using the Docker container image.

The deployment environment provides the required runtime configuration through environment variables, including:

- Database connection URL.
- Database username and password.
- JWT signing secret.
- Report JWT signing secret.
- Application port.

### Container Image Management

Docker images are built locally and published to **Docker Hub** before being deployed to the cloud environment.

This provides a clear separation between:

```text
Source Code
     ↓
Build
     ↓
Docker Image
     ↓
Container Registry
     ↓
Cloud Deployment
```

### Environment Configuration

Environment-specific configuration is externalized from the application source code.

Sensitive values such as database credentials and JWT secrets are injected at runtime through environment variables.

This prevents credentials and cryptographic secrets from being committed to the source repository.

## 🧩 Project Structure

The application follows a layered structure that separates presentation, business logic, persistence, security, and integration responsibilities.

```text

src/
└── main/
    ├── java/
    │   └── com/
    │       └── cotizador/
    │            ├─ configuration
    │            │  └─WebClientConfig                         [class]  
    │            ├─ controller
    │            │  └─api
    │            │   │    └─ RateApiController                [class]
    │            │   │    └─ RateViewController               [class]
    │            │   └─report
    │            │   │   └─ ReportController                  [class]
    │            │   ├─ AdminController                       [class]
    │            │   ├─ IndividualController                  [class]
    │            │   ├─ LoginController                       [class]
    │            │   ├─ PaymentCalculatorController           [class]
    │            │
    │            │
    │            ├── dao/
    │            │   ├── BrandsDAO.java                       [interface]
    │            │   ├── BrandsDAOImp.java                    [class]
    │            │   ├── ChargesDAO.java                      [interface]
    │            │   ├── ChargesDAOImp.java                   [class]
    │            │   ├── ChargesReceivableDAO.java            [interface]
    │            │   ├── ChargesReceivableDAOImp.java         [class]
    │            │   ├── HolidayRepository.java               [interface]
    │            │   ├── IndividualDAO.java                   [interface]
    │            │   ├── IndividualDAOImp.java                [class]
    │            │   ├── LegalEntitiesDAO.java                [interface]
    │            │   ├── LegalEntitiesDAOImp.java             [class]
    │            │   ├── ModelsDAO.java                       [interface]
    │            │   ├── ModelsDAOImp.java                    [class]
    │            │   ├── PaymentcalculatorDAO.java            [interface]
    │            │   ├── PaymentcalculatorDAOImp.java         [class]
    │            │   ├── PaymentDayDAO.java                   [interface]
    │            │   ├── PaymentDayImp.java                   [class]
    │            │   ├── ProcessDAO.java                      [interface]
    │            │   ├── ProcessDAOImp.java                   [class]
    │            │   ├── RateDAO.java                         [interface]
    │            │   ├── RateDAOImp.java                      [class]
    │            │   ├── ResidualValueDAO.java                [interface]
    │            │   ├── ResidualValueDAOImp.java             [class]
    │            │   ├── RoleDAO.java                         [interface]
    │            │   ├── RoleDAOImp.java                      [class]
    │            │   ├── ScheduledPaymentDAO.java             [interface]
    │            │   ├── ScheduledPaymentDAOJpaImp.java       [class]
    │            │   ├── SpreadDAO.java                       [interface]
    │            │   ├── SpreadDAOImp.java                    [class]
    │            │   ├── TaxesDAO.java                        [interface]
    │            │   ├── TaxesDAOImp.java                     [class]
    │            │   ├── UsersDAO.java                        [interface]
    │            │   ├── UsersDAOImp.java                     [class]
    │            │   ├── VehicleYearsDAO.java                 [interface]
    │            │   └── VehicleYearsDAOImpjava                 [class]
    │            │
    │            ├── entity/
    │            │   ├── BrandsDAOImp.java                    [class]      
    │            │   ├── ChargesDAOImp.java                   [class]
    │            │   ├── ChargesReceivableDAOImp.java         [class]
    │            │   ├── IndividualDAOImp.java                [class]
    │            │   ├── LegalEntitiesDAOImp.java             [class]
    │            │   ├── ModelsDAOImp.java                    [class]
    │            │   ├── PaymentcalculatorDAOImp.java         [class]
    │            │   ├── PaymentDayImp.java                   [class]
    │            │   ├── ProcessDAOImp.java                   [class]
    │            │   ├── RateDAOImp.java                      [class]
    │            │   ├── ResidualValueDAOImp.java             [class]
    │            │   ├── RoleDAOImp.java                      [class]
    │            │   ├── ScheduledPaymentDAOJpaImp.java       [class]
    │            │   ├── SpreadDAOImp.java                    [class]
    │            │   ├── TaxesDAOImp.java                     [class]
    │            │   ├── UsersDAOImp.java                     [class]
    │            │   └── VehicleYearsDAO.java                 [class]
    │            ├── exception/
    │            │   ├── CustomException.java                 [class]      
    │            │   ├── PaymentCalculatorErrorResponse.java  [class]
    │            │   ├── PaymentCalculatorNotFoundException.java  [class]
    │            │   └── PaymentCalculatorRestExceptionHandler.java [class]
    │            ├── integration
    │            │   │    └─banxico
    │            │   │      └─ BanxicoTiieeClient                  [class]
    │            │   │
    │            ├── security/
    │            │   │    └─jwt
    │            │   │       └─ SecurityConfig                     [class]
    │            │── service/
    │            │    ├── calculator/
    │            │    │      ├── FrenchInterestService.java        [class]      
    │            │    │      ├── InterestCalculator.java           [interface]
    │            │    │      └── PaymentCalculatorFactory.java     [class]
    │            │    ├── charges/
    │            │    │      ├── ChargeCalculatorProvider.java     [interface]      
    │            │    │      ├── ChargeService.java                [interface]
    │            │    │      ├── ChargeServiceImp.java             [class]      
    │            │    │      ├── ChargesReceivableService.java     [interface]
    │            │    │      ├── ChargesReceivableServiceImp.java  [class]      
    │            │    │      └── OpeningCommissionCalculator.java  [class]
    │            │    ├── facade/
    │            │    │      ├── LeadFacade.java                  [class]      
    │            │    │      ├── LeadSummaryFacade.java           [class]
    │            │    │      └── PaymentCalculatorFacde.java      [class]
    │            │    ├── rate/
    │            │    │      └── TiieDateService.java             [class]   
    │            │    │
    │            │    ├── BrandService.java                       [interface]
    │            │    ├── BrandServiceImp.java                    [class]
    │            │    ├── IndividualService.java                  [interface]
    │            │    ├── IndividualServiceImp.java               [class]
    │            │    ├── InterestDateService.java                [class]
    │            │    ├── LeadSummaryService.java                 [class]
    │            │    ├── LegalEntityService.java                 [interface]
    │            │    ├── LegalEntityServiceImp.java              [class]
    │            │    ├── ModelService.java                       [interface]
    │            │    ├── ModelServiceImp.java                    [class]
    │            │    ├── PaymentcalculatorService.java           [interface]
    │            │    ├── PaymentcalculatorServiceImp.java        [class]
    │            │    ├── PaymentDayService.java                  [interface]
    │            │    ├── PaymentDayServiceImp.java               [class]
    │            │    ├── ProcessService.java                     [interface]
    │            │    ├── ProcessServiceImp.java                  [class]
    │            │    ├── RateService.java                        [interface]
    │            │    ├── RateServiceImp.java                     [class]
    │            │    ├── ReportPDFService.java                   [class] 
    │            │    ├── ReportTokenService.java                 [class]
    │            │    ├── ResidualValueService.java               [interface]
    │            │    ├── ResidualValueServiceImp.java            [class]
    │            │    ├── RoleService.java                        [interface]
    │            │    ├── RoleServiceImp.java                     [class]
    │            │    ├── ScheduledPaymentService.java            [interface]
    │            │    ├── ScheduledPaymentServiceJpaImp.java      [class]
    │            │    ├── SpreadService.java                      [interface]
    │            │    ├── SpreadServiceImp.java                   [class]
    │            │    ├── TaxeService.java                        [interface]
    │            │    ├── TaxeServiceImp.java                     [class]
    │            │    ├── UserService.java                        [interface]
    │            │    ├── UserServiceImp.java                     [class]
    │            │    ├── VehicleYearService.java                 [interface]
    │            │    └── VehicleYearsServiceImp.java             [class]
    │            └── validator/
    │                ├── IndividualFormValidator.java             [class]      
    │                ├── IntValidator.java                        [class]
    │                └── ValidIndividualForm.java                 [interface]
    │
    └── resources/
        ├── reports/
        ├── static/
        ├── templates/
        └── application.properties
```

### Package Responsibilities

| Package | Responsibility |
|---|---|
| `controller` | Handles HTTP requests and coordinates application flows. |
| `service` | Contains application and business logic. |
| `service.calculator` | Implements the financial calculation and quotation logic. |
| `service.facade` | Provides application-level orchestration between controllers and business services. |
| `service.rate` | Handles interest-rate related services and external rate integration. |
| `dao` | Provides data-access functionality and custom persistence operations. |
| `entity` | Contains JPA entities representing the application's domain model. |
| `security` | Contains Spring Security and JWT-related configuration and components. |
| `resources/templates` | Contains Thymeleaf templates used by the web interface. |
| `resources/reports` | Contains compiled JasperReports templates used to generate PDF documents. |
| `resources/static` | Contains static web resources such as CSS, JavaScript, and other frontend assets. |

### Application Layers

The main application responsibilities can be summarized as:

```text
┌─────────────────────────────┐
│       Presentation          │
│   Thymeleaf / Controllers   │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│       Business Layer        │
│ Services / Facades /        │
│ Financial Calculation       │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│       Persistence           │
│       DAO / JPA / Hibernate  │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│           MySQL             │
└─────────────────────────────┘
```


## 🧮 Financial Calculation Flow


The quotation process is designed to separate request handling, business orchestration, financial calculation, and persistence.


A simplified flow is:


```text
User
  │
  ▼
Quotation Request
  │
  ▼
PaymentCalculatorController
  │
  ▼
PaymentCalculatorFacade
  │
  ▼
PaymentCalculatorFactory
  │
  ├──────────────────────┬──────────────────────┐
  ▼                      ▼                      ▼
Fixed Rate           Variable Rate        Pure Leasing
Calculation          Calculation          Calculation
  │                      │                      │
  │                      ▼                      │
  │                 BANXICO Rate               │
  │                      +                     │
  │                Financial Margin            │
  │                      │                      │
  └──────────────────────┴──────────────────────┘
                         │
                         ▼
               QuoteCalculatorService
                         │
                         ▼
              Amortization Schedule
                         │
                         ├── Payment Date
                         ├── Principal
                         ├── Interest
                         ├── Charges
                         ├── Residual Value
                         └── Outstanding Balance
                         │
                         ▼
                  Persistence Layer
                         │
                         ▼
                       MySQL
Financing Scenarios

The calculation engine supports different financing scenarios:

Fixed Rate

The configured fixed interest rate is used as the basis for calculating the periodic payments and amortization schedule.

Variable Rate

For variable-rate financing, the calculation uses a reference rate obtained through the BANXICO integration and adds the configurable financial margin:

Base Rate = BANXICO Reference Rate + Financial Margin

The resulting base rate is then used by the calculation engine to generate the amortization schedule.

Pure Leasing with Residual Value

For pure leasing scenarios, a residual value can be configured as a percentage of the vehicle value.

For example:

Vehicle Value:       $1,000,000
Residual Value:        $400,000

The residual amount remains as the final balance of the amortization schedule. At the end of the agreement, the customer may have the right to acquire the vehicle for the configured residual amount, according to the applicable contract conditions.

Configurable Business Rules

The calculation process also incorporates configurable business rules maintained through the administration module:

Payment due day.
Maximum vehicle age allowed for financing.
Financial margin for variable-rate products.
Residual value parameters.
Automatic processes.

🧪 Testing & Quality

The project includes automated tests focused on validating service-layer behavior, business validations, exception handling, DAO interactions, and selected web-layer workflows.

Testing Stack
Technology	Purpose
JUnit 5	Unit testing framework
Mockito	Mocking dependencies and verifying interactions
Spring MVC Test	Testing Spring MVC controllers using MockMvc
Unit Testing

Service-layer tests use JUnit 5 and Mockito to isolate business services from their data-access dependencies.

Current tests cover services such as:

Brand management.
Charge management.
Individual management.
Vehicle model management.
Payment calculator management.

The tests cover scenarios including:

Successful operations.
Invalid identifiers.
Null input validation.
Entity-not-found scenarios.
Create, update, and delete operations.
DAO interaction verification.
Expected exception handling.

A typical service test isolates the DAO using Mockito:

Service
   │
   │ uses
   ▼
Mock DAO
   │
   └── Controlled test response
          │
          ▼
       Assertions
          │
          ▼
   Interaction Verification
Web Layer Testing

Selected controller workflows are tested using Spring MVC Test and MockMvc.

Current controller tests include scenarios such as:

Form validation failures.
Successful lead creation.
View resolution.
Service interaction verification.
Facade interaction verification.

This allows controller behavior to be tested without requiring the complete application context.

Testing Approach

The current testing strategy focuses on validating both successful and failure scenarios rather than only testing the expected "happy path".

Examples include:

Valid and invalid identifiers.
Existing and non-existing entities.
Null input.
Validation failures.
Expected exceptions.
Verification that invalid requests do not reach the persistence layer.
Testing Roadmap

The testing strategy can be further expanded to provide broader coverage of the application's most critical components.

Planned areas include:

Financial calculation engine.
Fixed-rate calculations.
Variable-rate calculations.
BANXICO rate integration.
Residual value calculations.
Business rule validation.
Spring Security and JWT flows.
Database integration tests.
PDF report generation.
End-to-end quotation workflows.

## 🚀 Getting Started

This repository is a **showcase and technical documentation project** for the Automotive Financing Platform.

The complete application source code is maintained separately and is not included in this public repository.

### 🌐 Explore the Live Application

The platform is deployed on Railway and can be accessed through the following URL:

**Live Demo:**  
https://cotizador-production-0680.up.railway.app/creditos/automotriz/simulador

The live environment allows visitors to explore the automotive financing quotation workflow and review the application's user interface and generated results.

### 📚 Explore the Architecture

This repository provides technical documentation covering:

- Business problem and solution overview.
- Application architecture.
- Financial calculation flow.
- Technology stack.
- Security architecture.
- REST API documentation.
- Project structure.
- Testing strategy.
- Deployment infrastructure.

### 🖥️ Running the Application

The application was developed and tested locally using:

- Java 17.
- Spring Boot 3.3.
- Maven.
- MySQL 8.
- Docker.
- Docker Compose.

The application can also be packaged as a Docker image and deployed to a cloud environment.

> **Note:** The complete source code and environment-specific configuration are intentionally not included in this public showcase repository.

## 🎯 Project Goals & Future Improvements

The main goal of the project is to evolve the **Automotive Financing Platform** into a more complete financial quotation and customer engagement solution while continuing to improve its architecture, testing strategy, and business capabilities.

### 🧪 Expand Automated Testing

Continue increasing automated test coverage, with particular emphasis on the most business-critical components:

* Financial calculation engine.
* Fixed-rate calculations.
* Variable-rate calculations.
* Residual value calculations.
* Business rule validation.
* Early principal payments.
* Security and JWT flows.
* Database integration tests.
* End-to-end quotation workflows.

### 💰 Early Principal Payments

Implement support for additional principal payments during the financing term.

For example, a customer could make an additional **$30,000 principal payment in December**. The system would recalculate the remaining amortization schedule based on the new outstanding principal balance.

The feature could support different recalculation strategies, such as:

* Reducing the remaining term while maintaining a similar payment amount.
* Reducing the periodic payment while maintaining the original term.
* Allowing the user to select the desired recalculation strategy.

This functionality would extend the financial calculation engine beyond the initial quotation and allow the platform to model changes that occur during the life of a credit.

### 📧 Email Quotation Delivery

Allow customers to request their quotation to be delivered by email.

The generated PDF quotation could be sent automatically after the calculation process, providing a convenient way for the prospect to retain and review the proposal.

### 📱 Prospect Verification

Evaluate the implementation of a one-time verification code sent to the prospect's mobile phone during the initial quotation process.

The objective would be to verify that the provided contact information belongs to a real user and reduce invalid or automated submissions.

The implementation would be designed to balance:

* Prospect experience.
* Fraud and abuse prevention.
* Verification reliability.
* Operational cost.

### 👥 Prospect Management & Follow-up

Introduce a centralized prospect report containing users who have generated quotations.

The objective is to provide authorized users with a simple way to identify prospects who may require personal follow-up.

Potential information could include:

* Prospect information.
* Contact details.
* Date of quotation.
* Vehicle information.
* Financing product.
* Quotation amount.
* Financing term.
* Quotation status.
* Follow-up status.

This could evolve into a lightweight lead-management workflow within the platform.

### 📊 Flexible Financing Term Selection

Improve the financing-term selector by replacing the current predefined options with a more flexible month-based control.

A slider could allow users to select the desired financing term within the supported range while providing immediate visual feedback of the selected number of months.

### 🏠 Additional Financial Products

Expand the financial calculation engine beyond automotive financing.

Potential future products include:

* Mortgage financing.
* Personal loans.
* Other installment-based credit products.

The objective would be to evolve the calculation architecture so that different financial products can reuse common calculation components while implementing their own product-specific rules.

### 🔄 Continuous Architecture Improvement

Continue improving the application's architecture and engineering practices through:

* Increased automated testing.
* Database migration management.
* Improved API documentation.
* CI/CD automation.
* Improved observability and application monitoring.
* Additional validation and error handling.
* Refactoring toward greater separation of business rules and financial calculation logic.



