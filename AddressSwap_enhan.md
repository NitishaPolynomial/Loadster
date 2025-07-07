```mermaid
graph TD
    A[Start Testing] --> B{Are Pickup & Drop Addresses Present?}
    
    B -- No --> B1[Enter Only One Address]
    B1 --> B2[Click Swap Button]
    B2 --> B3[Verify: Swap Button is Disabled]

    B -- Yes --> C[Click Swap Button]
    C --> D1[Verify UI Alignment and Functionality]
    D1 --> D2[Verify Pickup and Drop are Swapped]

    D2 --> E[Manually Modify Drop Address]
    E --> F[Click Swap Again]
    F --> G[Verify Updated Drop is Now Pickup]

    G --> H[Check Fare Recalculation]
    H --> I[Fare Should Update Based on New Route]

    I --> J[Click Add Multiple Pickup/Drop]
    J --> K[Add New Location]
    K --> L[Verify Swap Still Effective with New Location]

    L --> Z[End Testing]
