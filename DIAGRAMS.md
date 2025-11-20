graph TB
    subgraph System["Infinity Gym Website System"]
        UC1[View Facility Information]
        UC2[View Trainer Profiles]
        UC3[Browse Membership Plans]
        UC4[Subscribe to Membership]
        UC5[Submit Contact Message]
        UC6[Search for Information]
        UC7[Admin Login]
        UC8[Manage Subscribers]
        UC9[View Contact Messages]
        UC10[Export Subscriber Data]
        UC11[Add New Subscriber]
        UC12[Edit Subscriber Information]
        UC13[Delete Subscriber]
        UC14[View Operating Hours]
        UC15[View Location]
    end
    
    Visitor[👤 Visitor/Member]
    Admin[👨‍💼 Admin]
    Firebase[(Firebase Database)]
    EmailJS[📧 EmailJS Service]
    
    Visitor -->|browses| UC1
    Visitor -->|views| UC2
    Visitor -->|explores| UC3
    Visitor -->|submits| UC4
    Visitor -->|sends| UC5
    Visitor -->|uses| UC6
    Visitor -->|checks| UC14
    Visitor -->|views| UC15
    
    Admin -->|authenticates| UC7
    Admin -->|performs| UC8
    Admin -->|reviews| UC9
    Admin -->|generates| UC10
    Admin -->|creates| UC11
    Admin -->|modifies| UC12
    Admin -->|removes| UC13
    
    UC4 -.->|stores data| Firebase
    UC5 -.->|stores data| Firebase
    UC8 -.->|reads/writes| Firebase
    UC9 -.->|reads| Firebase
    UC11 -.->|writes| Firebase
    UC12 -.->|updates| Firebase
    UC13 -.->|deletes| Firebase
    
    UC5 -.->|sends email| EmailJS
    
    style System fill:#120602,stroke:#fda312,stroke-width:3px,color:#fff
    style Visitor fill:#3b82f6,stroke:#1e40af,color:#fff
    style Admin fill:#bc3b10,stroke:#7c2d0a,color:#fff
    style Firebase fill:#fda312,stroke:#bc3b10,color:#000
    style EmailJS fill:#22c55e,stroke:#16a34a,color:#000
