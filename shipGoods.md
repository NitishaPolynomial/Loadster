```mermaid
flowchart TD
    Z["Start"] --> A{"User Authenticated?"}
    A -- No --> B["Authenticate Again"]
    A -- Yes --> C["Go to Dashboard"]
    C --> D{"Does User Want to Ship Goods?"}
    D -- No --> E["Continue Using App"]
    D -- Yes --> F@{ label: "Go to 'Ship Your Goods' Screen" }
    F --> G@{ label: "Selected 'Schedule Now' for Goods Pickup?" }
    G -- Yes --> H["Select Pickup Address
    Validation - 
    1. Ensure the entered postal code is correct for the selected region.
    2. Ensure the address is within serviceable locations."]
    G -- No --> I1["Select Schedule Date
    Validation - 
    1. Only current date & Future dates are allowed.
    2. Past dates are not allowed.
    3. Date format must be standard."]
    I1 -- Invalid Date --> I2@{ label: "Show 'Invalid Date' Error" }
    I1 -- Valid Date --> K1@{ label: "Select Time Slot\n    Validation -\n    1. Time should follow a proper format.\n    2. Users shouldn't be able to select a past time slot.\n    3. Ensure the slot follows a predefined duration (e.g., 30 min, 1 hour).\n    4. Prevent booking if the slot is already full." }
    K1 -- Invalid Slot --> K2@{ label: "Show 'Invalid Time Slot' Error" }
    K1 -- Valid Slot --> M{"Is Date & Time Preference Saved?"}
    M -- Yes --> H
    M -- No --> N["Ask for Date & Time Again"]
    H --> O["Search on Map
    Validation -
    1. The entered address exists and can be mapped.
    2. Select an address from the Google Maps autocomplete dropdown.
    3. Location services are enabled for accurate search results."] & P["Select Pin on Map
    Validation -
    1. Only Numbers are allowed, no letters and special characters are allowed.
    2. It should match the standard length based on the country.
    3. It falls within the correct range of valid pincodes for the selected country/region.
    4. The pincode should be within serviceable areas."] & Q["Select from Saved Address"]
    Q --> S{"Saved Address Exists?"}
    S -- No --> T["Add New Address with Tag, Lat/Long, Address Description"]
    S -- Yes --> U["Select Drop Location"]
    P --> U
    O --> U
    U --> V{"Multiple Drop Locations?"}
    V -- Yes --> W["Select Multiple Drop Addresses (Same Steps as Pickup)"]
    V -- No --> X["Select One Drop Address (Same Steps as Pickup)"]
    W --> Y1["Enter Contact Number
    Validations-
    1. Phone number must contain only numbers. No Alphbets and special characters are allowed other than +.
    2. Phone number must be exactly 10 digits, excluding country code.
    3. Phone number should not start with zero."]
    Y1 --> Y2["Enter Name
    Validation -
    1. Name must be between 2 and 200 characters.
    2. Allow only A-Z, a-z, and spaces (no numbers or special characters).
    3. Restrict @, #, $, %, 123, etc.
    4. No leading and trailing spaces are allowed.
    5. Auto case sensitivity should be applied."]
    Y2 --> Y3["Enter Delivery Instruction"]
    X --> Y1
    Y3 --> AB{"Skip Goods Information?"}
    AB -- Yes --> AC["Vehicle Types View: TATA Ace, TATA 407, 8ft Pickup, 3 Wheeler, 2 Wheeler"]
    AB -- No --> AD1["Select Goods Category
    Validaions - 
    1.  Ensure the selected category exists in the predefined list.
    2. Block restricted or hazardous goods if not allowed.
    3. In others - Restrict invalid characters like @, #, $, 123."]
    AD1 --> AD2["Select Goods Type
    Validations -
    1. The chosen type must match a predefined list.
    2.  If certain goods types are restricted (e.g., hazardous, flammable), verify permissions.
    3. In others - Restrict special characters and numbers in manually entered goods types.
    4. Goods type must be between 3 and 100 characters."]
    AD2 --> AD3["Enter Package Dimensions
    Validationns -
    1. Length, Width, Height, and Unit must be provided.
    2. Only allow numbers (no letters or special characters except decimal points).
    3. Dimensions must be greater than zero.
    4. Allow only predefined units (cm, inch, mm, feet).
    5.  If total volume (L × W × H) exceeds the limit, prevent submission.
    6. Restrict unnecessary decimal places (e.g., max 2 decimal places).
"]
    AD3 --> AD4["Enter Package Weight
    Validation -
    1. f the checkbox is checked, weight input must be provided and valid.
    2. Ensure the checkbox is not conflicting with other weight-related inputs (e.g., pre-filled weights).
    3. Estimated weight is not valid for the selected goods category."]
    AD4 --> AD5["Enter Total Value of Goods
    Validation -
    1. Allow only numbers (no letters or special characters except decimal points).
    2. Value must be greater than zero.
    3. Total value exceeds the maximum allowed limit.
    4. Only two decimal places are allowed.
    5. If the value exceeds a certain threshold, prompt for mandatory insurance selection."]
    AD5 --> AD6["Select Insurance Status
    Validations - 
    1. Ensure the checkbox is checked if insurance is compulsory for high-value goods.
    2. Insured amount cannot exceed the total value of goods.
    3. "]
    AD6 --> AE{"Goods Information Saved?"}
    AE -- No --> AF["Show Validation Errors"]
    AE -- Yes --> AC
    AC --> AG{"Additional Services Required?"}
    AG -- Yes --> AH1["Select Loading & Unloading
    Validations -
    1. If selected, Only Loading and Only Unloading should be disabled to prevent duplicate charges
    2. Ensure the total price is updated accordingly.
    3. An error message should be displayed You cannot select 'Only Loading' or 'Only Unloading' if 'Loading and Unloading' is already selected."] --> AH2["Select Only Loading
    Validations - 
    1. If selected, Loading and Unloading should be disabled (as it's a combined service).
    2. If both Only Loading and Only Unloading are selected, ensure the total cost equals ₹800 (same as combined service).
    "] --> AH3["Select Only Unloading
    Validations -
    1. If selected, Loading and Unloading should be disabled."] --> AH4["Select Proof of Delivery (Pricing Applies)
    Validations -
    1. Optional, can be selected with any combination of the above services.
    2. Ensure that the total price updates correctly when this option is added."]
    AG -- No --> AI["Continue with Selected Vehicle Type"]
    AH4 --> AJ["Review Details: Pickup, Drop, Preferences"]
    AH3 --> AJ
    AH2 --> AJ
    AH1 --> AJ
    AI --> AJ
    AJ --> AK["Payment Summary Page
    Validations -
    1. Ensure selected services and pricing are accurately displayed.
    2. Validate subtotal, taxes, discounts, and final amount.
    3. Prevent checkout if no payment method is chosen.
    4. Ensure only applicable and unexpired promo codes are applied.
    5. Disable the confirm button after one click to avoid double transactions."]
    AK --> AL{"Is Payment Successful?"}
    AL -- No --> AM["Show Payment Failure & Retry Option"]
    AL -- Yes --> AN["Show Confirmation & Order Summary"]

    F@{ shape: rect}
    G@{ shape: rect}
    I2@{ shape: rect}
    K1@{ shape: rect}
    K2@{ shape: rect}

 ```
