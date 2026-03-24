## Data Flow Diagram (DFD)

```mermaid
flowchart TD

    USER["Customer / Merchant"]

    subgraph INTERNET["Internet (Untrusted Zone)"]
        CLIENT["Web / Mobile Client"]
    end

    subgraph BACKEND["Backend (Trusted Zone)"]
        API["API Gateway"]
        AUTH["Auth Service"]
        PAY["Payment Service"]
        DB[("Database")]
    end

    THIRD["Third-Party Payment Processor"]

    USER -->|"HTTPS TLS"| CLIENT
    CLIENT -->|"API Requests"| API
    API --> AUTH
    API --> PAY
    PAY -->|"Store / Retrieve"| DB
    PAY -->|"Payment Request"| THIRD
