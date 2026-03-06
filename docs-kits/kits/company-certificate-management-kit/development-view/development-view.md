---
title: Development View
sidebar_position: 1
---

## Development View

![Company Certificate Management KIT Icon](@site/static/img/kits/company-certificate-management/ccm-kit-logo.svg)

Technical documentation for developers, architects, and implementers.

:::info Target Audience
Software Developers, Solution Architects, Technical Leads, API Developers, Integration Engineers.
:::

---

### More Guides

- [Architecture & CCMAPI Guide](architecture.md)

---

## Functional Requirements

### Core Functionalities

#### Certificate Lifecycle Management

- Creation, update, renewal, and expiration tracking of certificates.
- Upload and storage of digital certificate documents.
- Association of certificates with specific business partners and company records.

#### Validation and Approval Workflows

- Automated and manual validation of certificate authenticity.
- Multi-step approval processes involving different roles (e.g., business partner manager, compliance officer).
- Notifications and escalation for pending approvals or expiring certificates.

#### Integration with Master Data

- Synchronization with business partner master data (e.g., SAP, ERP systems).
- Automatic linking of certificates to business partner records.

#### Audit and Reporting

- Logging of all actions for audit trails.
- Generation of compliance and status reports (e.g., list of expired/missing certificates).
- Export of reports for external audits.

#### User and Role Management

- Role-based access control (RBAC) for different user groups (e.g., admin, approver, viewer).
- Delegation and substitution management for approvals.

#### Notifications and Alerts

- Automated email or system notifications for certificate expiry, missing documents, or workflow tasks.
- **API endpoints and resources**:
  - Company Certificate Request
  - Company Certificate Push
  - Company Certificate Status (Accepted / Received / Rejected)
  - Company Certificate Available
  - Error Handling
- Dashboard for monitoring certificate status and pending actions.

#### Document Management

- Secure upload, storage, and retrieval of certificate files.
- Versioning and history tracking for certificate documents.

---

## Non-Functional Requirements

### Quality Attributes

#### Security

- Data encryption at rest and in transit.
- Strict access controls to sensitive certificate data.
- Compliance with relevant data protection regulations (e.g., GDPR).

#### Scalability

- Ability to handle a large number of business partners and certificates.
- Support for future integration with additional systems or modules.

#### Reliability & Availability

- High system uptime to ensure business continuity.
- Backup and disaster recovery mechanisms.

#### Performance

- Fast response times for certificate lookups and workflow actions.
- Efficient batch processing for notifications and reporting.

#### Usability

- Intuitive user interface for both business and technical users.
- Multilingual support if required by the business context.

#### Auditability

- Comprehensive logging of all user actions and system events.
- Tamper-proof audit trails for compliance verification.

#### Maintainability

- Modular architecture to support easy updates and enhancements.
- Clear documentation for system configuration and operation.

#### Integration

- Standard APIs or connectors for integration with ERP, CRM, and document management systems.
- Support for importing/exporting data in standard formats (e.g., CSV, XML).

---

## Terminology

This section is non-normative. In this section the different parts of the data model are explained.

### BPNL – Business Partner Number Legal Entity

A Business Partner Number Legal Entity (BPNL) represents and uniquely identifies a Legal Entity, which is defined by its legal name (including Legal Form, if registered), legal Address and Tax Number. For further details on BPNLs please see standard CX-0010:2.0 Business Partner Number.

For this standard and the data model the BPNL is the BPN id of the certified legal entity (on which the certificate is issued).

**Attribute**: `businessPartnerNumber`

### Certificate Type

The attribute `CertificateType` refers to the type of the certificate the BPN is certified for. This data model is generic and currently supports, but is not limited to, the following list of certificate types. Additional certificate types will be validated in the future, and others may already be compatible with this generic model:

- **IATF 16949** (International Automotive Task Force) – A standard that defines the requirements for a quality management system in the automotive industry.
- **ISO 14001** – A standard that outlines the requirements for an environmental management system to help organizations minimize their impact on the environment.
- **ISO 9001** – A standard that sets out the requirements for a quality management system to help organizations consistently provide products and services that meet customer and regulatory requirements.
- **ISO 45001, OHSAS 18001 or national certification** – Occupational health and safety management system standards that help companies identify and manage workplace hazards to prevent accidents and injuries.
- **ISO/IEC 27001** – An information security management system standard that provides a framework for companies to manage and protect their sensitive information.
- **ISO 50001 or national certification** – An energy management system standard that helps companies improve energy efficiency and reduce costs.
- **ISO/IEC 17025** – A laboratory accreditation standard that ensures the accuracy and reliability of testing and calibration results.
- **ISO 20000** – An IT service management system standard that helps companies deliver high-quality IT services to their customers.
- **ISO 22301** – A business continuity management system standard that helps companies prepare for and respond to unexpected disruptions to their operations.
- **AEO (Authorized Economic Operator), CTPAT, Security Declaration** – Internationally recognized certificates that confirm a company's compliance with customs regulations and supply chain security standards.
- **VDA6.4** – A standard that defines the requirements for a quality management system in the automotive industry, with a focus on process auditing.

:::note
The spelling of the certificate type may vary slightly on the user interface or within the data model.
:::

### Registration and Issuing

The issuing authority is the authority that issues a certificate – e.g. TUEV Sued. The registration number is the unique identifier of the certificate at the certification authority / issuing body.

**Example**: ISO 9001 certificate is issued by TUEV Süd, which is the certification authority.

### Area of Application

The attribute `areaOfApplication` refers to the area of applications for the given certification, i.e. additional details.

### Enclosed Sites / Addresses

The attribute `enclosedSites` is closely linked to the Business Partner Number (BPN) and indicates additional sites, such as production or engineering sites, that are covered by the certificate. In other words, the certificate is valid not only for the primary BPN, but also for any associated sites (BPNS). This attribute is particularly useful for companies with multiple locations or business units, as it allows them to manage certificates more efficiently and ensures that all relevant sites are covered by the certificate.

:::note
If no BPNS is available, the use of the Business Partner Number Address (BPNA) is also allowed within this attribute.
:::

### Validity

The attribute validity refers to the date from which the certificate is valid. If it is not defined, it is recommended to use the date of issue/signature of the document. In connection with the valid-from date, there is the valid-to date for a certificate – 31.12.9999 for no expiration date.

### Trust Level

This data object defines the trust level of the certificate.

The certificates are provided in the business context by the company itself – they are showing their certificates to other companies. Not every certificate can be directly validated by the issuing authority. That is why there are different trust levels defined:

| Trust Level | Description |
|-------------|-------------|
| **None** | No validation check at all, just uploaded / provided by the company. |
| **Low** | Manual validation check done by human after upload. |
| **Medium** | Certificate provided by trusted issuer and manually checked (as low). |
| **High** | Automated cross check via some database (e.g. TÜV, IATF). |
| **Trusted** | Directly provided by issuer (e.g. TÜV). |

### Validator

The validator is the one who can validate certificate information. In the best way it is the authority that is issuing the certificates but there can be other validators. This attribute has a relation to the trust level.

E.g. Business service providers that offer a validation service for company certificates.

:::note
The property `validatorBpn` expects the BPNL as the default. However, if deemed necessary, this property can be used as a free text field (string).
:::

### Certificate Uploader

The attribute `uploader` defines the company (uploader) who originally provided the given certificate (e.g. company A provided it to business application provider B, business application provider B is a trusted validator). This company is also identified by a BPN.

### Document ID

The internal reference id to request a certificate document.

---

## NOTICE

This work is licensed under the [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/legalcode).

- SPDX-License-Identifier: CC-BY-4.0
- SPDX-FileCopyrightText: 2025 Contributors to the Eclipse Foundation
- Source URL: [https://github.com/eclipse-tractusx/eclipse-tractusx.github.io](https://github.com/eclipse-tractusx/eclipse-tractusx.github.io)

