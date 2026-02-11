# THreat modeling Report

1 Application Overview
Applocation name: PayNow
Application in Scope: Payment Processing & Card Storage
Primary Users:
* Customers
* Merchants
* Internal Support Staff

Objective of this Threat Model:
Identify realistic security threats affacting payment processcing and card storage, assess risk, and propose mitigations early in the SDLC.

2 Architecture Overview
Key Components
* Web/MObile Client
* API Gateway
* Payment Service
* Database(Users, Cards, Transactions)
* Third-party Payment Processor

Sensitive Data
* Credit card numbers
* Transaction history
* User PII 
* API key/secrets

3 Assets at Risk
* Credit Card Numbers | Financial fraud risk
* User PII | Identity theft
* TransactionRecords | Fraud & financial manipulation
* API Keys | Full system compromise

* Data Flow Diagram(DFD)
 
 [ Customer / Merchant ]
            |
            | HTTPS (TLS)
            v
      [ Web / Mobile Client ]
            |
            v
        [ API Gateway ]
            |
      ---------------------
      |                   |
      v                   v
[ Payment Service ]   [ Auth Service ]
      |
      v
     [ Database ]
      |
      v
[ Third-Party Payment Processor ]

           
4 Trust Boundaries
Trust boundaries exit between:
 * Client - API Gateways
 * API Gate way - Internal Services
 * Payment Service - Database
 * PayNow - Yhird-party Payment Processor 
 * Internal Staff - Admin Interfaces
These boundaries represent points where authentication, authorization, and validation must occur.

5 Threat Identification
# Use STRIDE framework
* We used the STRIDE model to systematically identify threats across system components and trust boundaries.

Threat 1: Card Data Exposure
* What is at risk?
  i  Stored credit card numbers in the database
* Who cold exploit it?
  i   External attackers
  ii  Malicious insiders
  iii Compromised third-party vendors
* Why would they do it?
  i Finanacial fraud and card resale on dark web
* How could it realistically happen?
  i   SQL Injection
  ii  Database misconfiguration
  iii Broken access control
  iv  Unencypted card storage 
* Risk Assessment
   i   Imapct: High
   ii  Likelihood: Medium
   iii Overrall Risk: High

2 Threat 2: Unauthorized Payment Manipulation
* What is at risk?
  i Transaction integrity.
* Who could exploit this?
  i  Authenticated users abusing logic
  ii Attackers intercepting requests
* Why would they do it?
  i Financial gain(changing payment amount, replaying transactions)
* How would they do it?
  i   Parameter tempering 
  ii  Replay attacks
  iii Missing server-side validation
* Risk Assessment
  i   Impact: High
  ii  Likelihood: Medium
  iii Overall Risk: High

3 Threat 3: API Key Leakage
* What is at risk?
  i Third-party payment processor credentials 
* Who could exploit this?
  i  External attackers
  ii Developers accidentally commiting secrets
* Why would they do it?
  i To execute fraudulent transactions
* How would they do it?
  i  Hardcode secrets
  ii Exposed logs
  iii CI/CD misconfiguration
* Risk Assessment 
  i   Impact: Critical
  ii  likelihood: Medium
  iii Overall Risk: High 

6 Mitigation & Controls
1 Protect Card Data:
  i   Use PCI-DSS complaint tokenization
  ii  Ecrypt card data at rest(AES-256)
  iii Enforce TLS 1.2+ in transit
  iv  Apply strict RBAC on database access
2 Secure Payment Logic:
  i   Server-side validation of payment amount
  ii  Implement idempotency keys to prevent replay attacks
  iii Strong authentication (MFA for sensitive actions)
  iv  Implement proper authorization checks 
3 Protect Secrets & API Keys:
  i   Store secrets in secure vaults (e.g, HashiCorp Vault, AWS Secrets Manager)
  ii  Prevent hardcoding secrets
  iii Enbale secres scanning in CI/CD 
  iv  Rotate API Keys regularly

7 Additional Security Controls
  i   Rate limiting at API Gateway
  ii  Web Application Firewall (WAF)
  iii Input validation & output encoding
  iv  Logging & monitoring (SIEM integration)
  v   Least privilege access model


