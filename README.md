<div align="center">

# 🚗 Automotive Financing Platform

### Enterprise Web Application for Automotive Financing & Leasing

A cloud-native web application developed with **Spring Boot 3** that automates automotive financing quotations, leasing calculations, business rule management, and secure PDF proposal generation.

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

</div>
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

Administrative users can configure business parameters that influence the quotation process, including:

- Interest rates.
- Payment days.
- Vehicle age rules.
- Automatic processes.
- Other configurable business parameters.

This approach allows business rules to be modified without requiring changes to the application's source code.

#### 📄 PDF Quotation Generation

The platform generates professional PDF documents containing the quotation information and payment schedule using **JasperReports**.

Report access is protected through a dedicated JWT-based mechanism.

#### 🔐 Security & Administration

Administrative functionality is protected using **Spring Security**, with authentication and role-based authorization.

The application also exposes REST endpoints secured through JWT authentication for specific services.

#### 🌐 External Integration

The application integrates with **BANXICO** services through Spring WebClient to retrieve financial information used by the platform.
