# Infinity Gym System Diagrams

## 1. Use Case Diagram
This diagram outlines the interactions between the Visitor and the Admin.

```mermaid
usecaseDiagram
    actor "Website Visitor" as Visitor
    actor "Gym Admin" as Admin

    package "Infinity Gym Website" {
        usecase "View Home & Facilities" as UC1
        usecase "View Trainers" as UC2
        usecase "Submit Contact Form" as UC3
        usecase "Subscribe to Plan" as UC4
        usecase "Admin Login" as UC5
    }

    package "Admin Dashboard" {
        usecase "View Subscriber List" as UC6
        usecase "Add New Subscriber" as UC7
        usecase "Edit Subscriber" as UC8
        usecase "Delete Subscriber" as UC9
        usecase "Search Subscribers" as UC10
        usecase "Export Data to CSV" as UC11
        usecase "View/Delete Messages" as UC12
    }

    Visitor --> UC1
    Visitor --> UC2
    Visitor --> UC3
    Visitor --> UC4

    Admin --> UC5
    UC5 --> UC6
    Admin --> UC7
    Admin --> UC8
    Admin --> UC9
    Admin --> UC10
    Admin --> UC11
    Admin --> UC12
sequenceDiagram
    autonumber
    actor User as Visitor
    participant UI as Web Interface (index.html)
    participant JS as JavaScript Logic
    participant DB as Firebase Firestore

    User->>UI: Clicks "Subscribe" on Plan
    UI->>UI: Scrolls to Subscription Form
    UI-->>User: Displays Form (Plan Pre-selected)
    User->>UI: Fills Name, Email, Phone, Duration
    User->>UI: Clicks "Confirm & Pay"
    UI->>JS: Trigger submit event
    JS->>DB: db.collection('subscriptionRequests').add()
    
    alt Success
        DB-->>JS: Return Document ID
        JS->>UI: Show Success Message
        UI-->>User: "Subscription request sent!"
    else Error
        DB-->>JS: Return Error
        JS->>UI: Show Error Message
    end
sequenceDiagram
    autonumber
    actor Admin
    participant Dash as Admin Dashboard
    participant Auth as Auth Logic
    participant DB as Firebase Firestore

    Admin->>Dash: Enter Credentials
    Dash->>Auth: Validate (admin/password)
    
    alt Valid Credentials
        Auth-->>Dash: Access Granted
        Dash->>DB: db.collection('subscribers').get()
        DB-->>Dash: Return Subscriber List
        Dash-->>Admin: Display Dashboard Table
    else Invalid
        Auth-->>Dash: Show Error Message
    end

    Admin->>Dash: Fill "Add New Subscriber" Form
    Admin->>Dash: Click "Add Subscriber"
    Dash->>DB: db.collection('subscribers').add()
    DB-->>Dash: Return Success
    Dash->>Dash: Update Table UI
    Dash-->>Admin: Show "Subscriber added successfully"
flowchart TD
    A([Start]) --> B[User enters Contact Section];
    B --> C[User fills Name, Email, Subject, Message];
    C --> D[User clicks Send];
    D --> E{Form Valid?};
    
    E -- No --> F[Browser shows validation error];
    F --> C;
    
    E -- Yes --> G[JavaScript captures Data];
    G --> H[Save to Firebase 'contactMessages'];
    
    H --> I{Save Successful?};
    I -- Yes --> J[Display Success Message];
    I -- No --> K[Display Error Message];
    
    J --> L[Clear Form];
    L --> M([End]);
    K --> M;
