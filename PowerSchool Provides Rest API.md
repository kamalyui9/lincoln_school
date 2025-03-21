# PowerSchool Provides Rest API

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
    Odoo->>Odoo: Run Scheduler (Every 5 Min)
    Odoo->>PowerSchool: Call API to Get Student Data
    PowerSchool-->>Odoo: Send Student Data (JSON)
    Odoo->>Odoo: Extract Student Data
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
    Odoo->>Odoo: Prepare Employee/Teacher Data for Sync
    Odoo->>Odoo: Run Scheduler (Every 5 Min)
    Odoo->>PowerSchool: Call API to Post Teacher Data
    PowerSchool-->>Odoo: API Response (Success/Error)
    PowerSchool->>PowerSchool: Extract Teacher Data
    PowerSchool->>PowerSchool: Map Data to Create Teacher Record
    Odoo->>HR: Sync Confirmation & Error Handling
```

# 3. Sync Transactional Data (Enrollment & Billing) from PowerSchool to Odoo

```mermaid
sequenceDiagram
    participant Student as Student
    participant Admin as Admin
    participant PowerSchool as PowerSchool
    participant Odoo as Odoo
    participant Accounting as Accounting (Odoo)

    Student->>Admin: Enroll in Course
    Admin->>PowerSchool: Register Student & Generate Invoice
    PowerSchool->>PowerSchool: Prepare Enrollment & Billing Data for Sync
    Odoo->>Odoo: Run Scheduler (Every 5 Min)
    Odoo->>PowerSchool: Call API to Get Enrollment & Billing Data
    PowerSchool-->>Odoo: Send Enrollment & Billing Data (JSON)
    Odoo->>Odoo: Extract Enrollment & Billing Data
    Odoo->>Accounting: Map Data to Create Invoice in Odoo
    Odoo-->>Admin: Transaction Successfully Synced
```
