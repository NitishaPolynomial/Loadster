```mermaid
graph TD
    A[Start Testing] --> B[Is User Logged In and Location API Enabled?]
    B -- No --> X1[Fail: Cannot Test Location Suggestions]
    B -- Yes --> C[Click on Pickup or Drop Field]

    C --> D[Location Search Page Should Open]
    D --> E[Start Typing Sample Location]

    E --> F[Show Relevant Suggestions Below Input]
    F --> G[Check Suggestions Visibility on Screen]

    G --> H{Are More Than 4-5 Suggestions?}
    H -- Yes --> H1[Suggestions Should Be Scrollable]
    H -- No --> H2[All Suggestions Should Be Visible Without Scroll]

    F --> I[Tap a Suggestion From List]
    H1 --> I
    H2 --> I
    I --> J[Input Field Should Fill with Selected Location]

    F --> K[Clear the Input Field]
    K --> L[Suggestions Should Disappear]

    E --> M[Type Invalid Location Text]
    M --> N[Show Message: No Results Found]

    J --> Z[End Testing]
