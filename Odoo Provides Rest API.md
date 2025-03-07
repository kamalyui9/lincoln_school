# Odoo Provides Rest API

# 1. Sync Student/Parent Data from PowerSchool to Odoo
```mermaid
sequenceDiagram
    participant Student as Student
    participant Admin as Admin
    participant PowerSchool as PowerSchool
    participant Odoo as Odoo

    Student->>Admin: Apply for Enrollment
    Admin->>PowerSchool: Create Student Record
    PowerSchool->>PowerSchool: Prepare Student Data for Sync
    PowerSchool->>Odoo: Call Odoo API to POST Student Data
    Odoo-->>PowerSchool: API Response (Success/Error)
    Odoo->>Odoo: Extract & Process Student Data
    Odoo->>Odoo: Map Data to Create Contact in Odoo
    Odoo-->>Admin: Student Data Successfully Synced
```

# 2. Sync Employee/Teacher Data from Odoo to PowerSchool
```mermaid
sequenceDiagram
    participant HR as HR (Odoo)
    participant Odoo as Odoo
    participant PowerSchool as PowerSchool

    HR->>Odoo: Create/Update/Delete Employee (Teacher)
    Odoo->>Odoo: Prepare Employee Data for Sync
    PowerSchool->>Odoo: Call Odoo API to GET Teacher Data
    Odoo-->>PowerSchool: Send Teacher Data (JSON Response)
    PowerSchool->>PowerSchool: Extract & Process Teacher Data
    PowerSchool->>PowerSchool: Map Data to Create Teacher Record
    PowerSchool-->>Odoo: Sync Confirmation

```

# 3. Sync Transactional Data (Enrollment & Billing) from PowerSchool to Odoo
```mermaid
sequenceDiagram
    participant Student as Student
    participant Admin as Admin
    participant PowerSchool as PowerSchool
    participant Odoo as Odoo

    Student->>Admin: Enroll in Course
    Admin->>PowerSchool: Register Student & Generate Invoice
    PowerSchool->>PowerSchool: Prepare Enrollment & Billing Data for Sync
    PowerSchool->>Odoo: Call Odoo API to POST Enrollment & Billing Data
    Odoo-->>PowerSchool: API Response (Success/Error)
    Odoo->>Odoo: Extract & Process Enrollment & Billing Data
    Odoo->>Odoo: Map Data to Create Invoice in Odoo
    Odoo-->>Admin: Transaction Successfully Synced

```
