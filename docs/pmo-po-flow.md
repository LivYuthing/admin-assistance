# PMO & PO Workflow

กระบวนการทำงานร่วมกันระหว่าง PMO และ PO (Product Owner)

## ภาพรวมกระบวนการ

```mermaid
flowchart TD
    A([Start]) --> B[PO รับ Business Requirement]
    B --> C[PO เขียน User Stories\nและ Acceptance Criteria]
    C --> D{PMO Review\nProject Scope?}

    D -- ไม่ผ่าน --> E[PO แก้ไข Requirement]
    E --> C

    D -- ผ่าน --> F[PMO จัดทำ Project Charter]
    F --> G[PMO กำหนด Timeline\nและ Resource Plan]
    G --> H{Sponsor อนุมัติ?}

    H -- ไม่อนุมัติ --> I[ทบทวนและปรับแผน]
    I --> F

    H -- อนุมัติ --> J[PO จัดทำ Product Backlog\nและ Sprint Plan]
    J --> K[เริ่ม Sprint / Execution]

    K --> L[Daily Standup\nPO + Dev Team]
    L --> M[PMO ติดตาม Progress\nและ Status Report]

    M --> N{มี Issue\nหรือ Risk?}

    N -- ใช่ --> O[PMO บันทึก Issue/Risk Register]
    O --> P{ระดับความเสี่ยง\nสูง?}
    P -- ใช่ --> Q[Escalate ถึง Sponsor]
    Q --> R[ประชุม Steering Committee]
    R --> K
    P -- ไม่ --> K

    N -- ไม่ --> S{Sprint\nเสร็จสิ้น?}

    S -- ไม่ --> L
    S -- ใช่ --> T[Sprint Review\nPO Demo ให้ Stakeholders]

    T --> U[Sprint Retrospective]
    U --> V{โครงการ\nเสร็จสิ้น?}

    V -- ไม่ --> J
    V -- ใช่ --> W[PMO จัดทำ Project Closure Report]
    W --> X[Lessons Learned Session]
    X --> Y([End])
```

## รายละเอียดบทบาท

### PMO มีหน้าที่
- จัดทำและดูแล Project Charter, Timeline, Budget
- ติดตาม Progress และจัดทำ Status Report
- บริหาร Risk และ Issue
- รายงานต่อ Steering Committee / Sponsor

### PO มีหน้าที่
- รับและวิเคราะห์ Business Requirement
- เขียนและจัดลำดับ Product Backlog
- กำหนด Acceptance Criteria
- Demo ผลลัพธ์ให้ Stakeholders

## จุดตัดสินใจหลัก (Decision Gates)

| จุด | ผู้ตัดสินใจ | เกณฑ์ |
|-----|-----------|-------|
| PMO Review Scope | PMO Lead | ขอบเขตชัดเจน, วัดผลได้ |
| Sponsor Approval | Sponsor | Budget และ Timeline อนุมัติ |
| Risk Escalation | PMO + Sponsor | Risk Level = สูง หรือ สูงมาก |
| Project Closure | Sponsor + PMO | Deliverables ส่งมอบครบ |
```
