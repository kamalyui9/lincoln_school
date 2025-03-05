# Odoo will provide the Endpoint using Rest API

## 1. Sync Student/Parent Data from PowerSchool to Odoo
```mermaid
sequenceDiagram
    participant Student as Student
    participant Admin as Admin
    participant PowerSchool as PowerSchool
    participant Odoo as Odoo 

    Student->>Admin: Apply for Enrollment
    Admin->>PowerSchool: Create/Update Student/Parent Record
    PowerSchool->>PowerSchool: Mark Record as Pending Sync
    PowerSchool->>PowerSchool: Prepare Student/Parent Data ready for Sync
    Note left of Odoo: Odoo exposes REST API

    PowerSchool->>Odoo: Call Odoo API (POST /api/parents & /api/students)
    Odoo->>Odoo: Extract & Process Student/Parent Data
    Odoo->>Odoo: Map Data to Create Contact Record
    Odoo-->>PowerSchool: API Response (Success/Error)

    alt Success
        PowerSchool->>PowerSchool: Mark Record as Synced
    else Error
        PowerSchool->>PowerSchool: Log Sync Failure
        PowerSchool-->>Admin: Notify Sync Failure
    end
```

## 2. Sync Employee/Teacher Data from Odoo to PowerSchool
```mermaid
sequenceDiagram
    participant Admin as HR (Odoo)
    participant Odoo as Odoo
    participant PowerSchool as PowerSchool

    Admin->>Odoo: Create/Update Employee Record
    Odoo->>Odoo: Mark Record as Pending Sync
    Odoo->>Odoo: Prepare Employee Data ready for Sync
    Note right of Odoo: Odoo exposes REST API

    PowerSchool->>Odoo: Call Odoo API (GET /api/employees)
    Odoo->>Odoo: Process API Request
    Odoo-->>PowerSchool: Return Employee Data (JSON)
    
    PowerSchool->>PowerSchool: Extract & Process Employee Data
    PowerSchool->>PowerSchool: Map Data to Create Teacher Record
    Note right of Odoo: Odoo exposes REST API

    PowerSchool->>Odoo: Call Odoo API Response (POST /api/teacher/status)
    Odoo->>Odoo: Process API Request
    Odoo-->>PowerSchool: Return Response 200

    alt Success
        Odoo->>Odoo: Mark Record as Synced
    else Error
        Odoo->>Odoo: Log Sync Error
        Odoo-->>Admin: Notify Sync Failure
    end
```

3. Sync Transactional Data (Enrollment & Billing) from PowerSchool to Odoo
```mermaid
sequenceDiagram
    participant Student as Student
    participant Admin as Admin
    participant PowerSchool as PowerSchool
    participant Odoo as Odoo 

    Student->>Admin: Enroll in Course
    Admin->>PowerSchool: Register Student & Generate Invoice
    PowerSchool->>PowerSchool: Mark Record as Pending Sync
    PowerSchool->>PowerSchool: Prepare Enrollment/Billing Data ready for Sync
    Note left of Odoo: Odoo exposes REST API

    PowerSchool->>Odoo: Call Odoo API (POST /api/enrollments & /api/billings)
    Odoo->>Odoo: Extract & Process Enrollment/Billing Data
    Odoo->>Odoo: Map Data to Create Enrollment/Billing Record
    Odoo-->>PowerSchool: API Response (Success/Error)

    alt Success
        PowerSchool->>PowerSchool: Mark Record as Synced
    else Error
        PowerSchool->>PowerSchool: Log Sync Failure
        PowerSchool-->>Admin: Notify Sync Failure
    end
```
