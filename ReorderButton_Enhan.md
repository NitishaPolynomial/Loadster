```mermaid
graph TD
    A[Start Testing] --> B[User Logged In?]
    B -- No --> Z1[Fail: Cannot test Reorder]
    B -- Yes --> C[Go to Orders Tab]

    C --> D{Order Status}
    D --> D1[All Orders]
    D --> D2[In Review]
    D --> D3[Cancelled]
    D --> D4[Undelivered]
    D --> D5[Completed]

    D1 --> E1[Check Reorder Button Present]
    E1 --> F1[Click Reorder Button]
    F1 --> G1[Check UI Alignment & Click Functionality]
    G1 --> H1[Pass: Reorder functional for general orders]

    D2 --> E2[Check Reorder for In Review]
    E2 --> F2{Multi Pickup/Drop?}
    F2 -- No --> G2[Verify Pre-filled Locations]
    F2 -- Yes --> G3[Verify All Multi Pickup/Drop Addresses Pre-filled]

    D3 --> E3[Check Reorder for Cancelled Order]
    E3 --> F3[Verify Order Page with Previous Details]

    D4 --> E4[Check Reorder for Undelivered Order]
    E4 --> F4[Verify Order Page with Previous Details]

    D5 --> E5[Check Reorder for Completed Order]
    E5 --> F5[Verify Order Page with Previous Details]

    G1 --> H[After Reorder: Change Pickup Address]
    H --> I[Edit Pickup Address]
    I --> J[Check if Updated in Summary]

    J --> K[Edit Drop Address]
    K --> L[Check if Updated in Summary]

    L --> M{Multi Pickup/Drop?}
    M -- Yes --> N[Add More Pickup/Drop]
    N --> O[Verify New Points Added]

    M --> P[Remove Existing Address]
    P --> Q[Verify Address Removed and Price Updated]

    Q --> R[Enter Invalid Address]
    R --> S[App Should Prevent or Show Error]

    S --> T[Change Drop and Recheck Fare]
    T --> U[Verify Fare is Recalculated]

    U --> Z[End Testing]

