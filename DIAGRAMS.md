usecaseDiagram
    actor "Guest / Potential Member" as User
    actor "Gym Administrator" as Admin

    package "Infinity Gym System" {
        
        package "Public Interface" {
            usecase "View Landing Page" as UC1
            usecase "View Facilities & Trainers" as UC2
            usecase "Submit Contact Query" as UC3
            usecase "View Pricing Plans" as UC4
            usecase "Submit Subscription Request" as UC5
        }

        package "Admin Dashboard" {
            usecase "Admin Login" as UC6
            usecase "View Dashboard Analytics" as UC7
            usecase "Manage Subscribers" as UC8
            usecase "Search/Filter Members" as UC9
            usecase "Export Data (CSV)" as UC10
            usecase "Manage Contact Messages" as UC11
        }
    }

    User --> UC1
    User --> UC2
    User --> UC3
    User --> UC4
    User --> UC5

    Admin --> UC6
    Admin --> UC7
    Admin --> UC8
    Admin --> UC9
    Admin --> UC10
    Admin --> UC11

    note right of UC5 : Saves to 'subscriptionRequests' collection
    note right of UC8 : CRUD operations on 'subscribers' collection
