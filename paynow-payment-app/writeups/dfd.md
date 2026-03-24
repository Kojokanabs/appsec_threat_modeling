## Data Flow Diagram (DFD)

```mermaid
flowchart TD
    A["Customer / Merchant"] -->|"HTTPS TLS"| B["Web / Mobile Client"]
    B --> C["API Gateway"]
    C --> D["Payment Service"]
    C --> E["Auth Service"]
    D --> F[("Database")]
    F --> G["Third-Party Payment Processor"]
