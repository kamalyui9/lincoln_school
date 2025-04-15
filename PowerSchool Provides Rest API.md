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
    Odoo->>Odoo: Prepare Employee Data for Sync
    PowerSchool->>PowerSchool: Run Scheduler (Every 5 Min)
    PowerSchool->>Odoo: Call Odoo API to GET Teacher Data
    Odoo-->>PowerSchool: Send Teacher Data (JSON Response)
    PowerSchool->>PowerSchool: Extract & Process Teacher Data
    PowerSchool->>PowerSchool: Map Data to Create Teacher Record
    PowerSchool-->>Odoo: Sync Confirmation

```

# 3. Sync Transactional Data (Enrollment Fees) from PowerSchool to Odoo

```mermaid
sequenceDiagram
    participant Student as Student
    participant Admin as Admin
    participant PowerSchool as PowerSchool
    participant Odoo as Odoo
    participant Accounting as Accounting (Odoo)

    Student->>Admin: Enroll in Course
    Admin->>PowerSchool: Student Registration process
    PowerSchool->>PowerSchool: Prepare Enrollment Fees Data for Sync
    Odoo->>Odoo: Run Scheduler (Every 5 Min)
    Odoo->>PowerSchool: Call API to Get Enrollment Fees Data
    PowerSchool-->>Odoo: Send Enrollment Fees Data (JSON)
    Odoo->>Odoo: Extract Enrollment Fees Data
    Odoo->>Accounting: Map Data to Create Enrollment Data in Odoo
    Odoo-->>Admin: Transaction Successfully Synced
```
