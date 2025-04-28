# PowerSchool Provides Rest API

# 1. Sync Student/Parent Data from PowerSchool to Odoo
```mermaid
sequenceDiagram
    participant Student as Student
    participant Admin as Admin
    participant PowerSchool as PowerSchool
    participant Odoo as Odoo

    Student->>Admin: Apply for Enrollment
    Admin->>PowerSchool: Create Student/Parent Data
    PowerSchool->>PowerSchool: Prepare Student/Parent Data for Sync
    Odoo->>Odoo: Run Scheduler (Every midnight) / button to sync manually
    Odoo->>PowerSchool: Call API to Get Student/Parent Data
    PowerSchool-->>Odoo: Send Student/Parent Data (JSON)
    Odoo->>Odoo: Extract Student/Parent Data
    Odoo->>Odoo: Map Data to Create/Update Contact in Odoo
    Odoo-->>Admin: Student/Data Data Successfully Synced
```

# 1. Sync Manually Student/Parent Data from Odoo to Powerschool
```mermaid
sequenceDiagram
    participant Admin as Admin
    participant Odoo as Odoo
    participant PowerSchool as PowerSchool

    Admin->>Odoo: Update Student/Parent Data
    Odoo->>Odoo: Prepare Student/Parent Data for Sync
    Odoo->>Odoo: Button to sync manually based on Payload and spesific student ID
    Odoo->>PowerSchool: Call API to Push Student/Parent Data
    PowerSchool->>PowerSchool: Receive and Extract Student/Parent Data
    PowerSchool->>PowerSchool: Map Data to Create/Update Contact in Odoo
    PowerSchool-->>Admin: Student/Data Data Successfully Synced
```

# 2. Sync Employee/Teacher Data from Odoo to PowerSchool
```mermaid
sequenceDiagram
    participant HR as HR (Odoo)
    participant Odoo as Odoo
    participant PowerSchool as PowerSchool

    HR->>Odoo: Create/Update/Delete Employee (Teacher)
    Odoo->>Odoo: Prepare Employee/Teacher Data for Sync
    PowerSchool->>PowerSchool: Run Scheduler (Every 5 Min)
    PowerSchool->>Odoo: Call Odoo API to GET Employee/Teacher Data
    Odoo-->>PowerSchool: Send Employee/Teacher Data (JSON Response)
    PowerSchool->>PowerSchool: Extract & Process Employee/Teacher Data
    PowerSchool->>PowerSchool: Map Data to Create/Update Employee Record
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
    Odoo->>Odoo: Run Scheduler (Every Midnight) / button to manually sync
    Odoo->>PowerSchool: Call API to Get Enrollment Fees Data
    PowerSchool-->>Odoo: Send Enrollment Fees Data (JSON)
    Odoo->>Odoo: Extract Enrollment Fees Data
    Odoo->>Accounting: Map Data to Create/Update Enrollment in Odoo
    Odoo-->>Admin: Transaction Successfully Synced
```
