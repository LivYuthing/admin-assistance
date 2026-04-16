# Confluent User Management - Flowchart

ขั้นตอนการจัดการผู้ใช้งานใน Confluent: ตรวจสอบ, ลบ, และเพิ่มผู้ใช้งาน

## Flowchart

```mermaid
flowchart TD
    A([Start]) --> B[Login Confluent\nAdmin Console]
    B --> C[เข้าเมนู\nUser Management]

    C --> D{ต้องการทำอะไร?}

    %% ===== ตรวจสอบผู้ใช้งาน =====
    D -- ตรวจสอบการใช้งาน --> E[เลือก Users / Accounts]
    E --> F[ดูรายชื่อผู้ใช้งานทั้งหมด]
    F --> G[เลือก User ที่ต้องการตรวจสอบ]
    G --> H[ดู Role, Permission\nและสถานะการใช้งาน]
    H --> I{พบปัญหา\nหรือต้องดำเนินการ?}
    I -- ไม่มี --> Z1([End - ไม่มีการเปลี่ยนแปลง])
    I -- ต้องลบ --> D2
    I -- ต้องแก้ไข Role --> J[แก้ไข Role / Permission]
    J --> K[บันทึกการเปลี่ยนแปลง]
    K --> Z2([End - อัปเดตสำเร็จ])

    %% ===== ลบผู้ใช้งาน =====
    D -- ลบผู้ใช้งาน --> D2[ค้นหา User ที่ต้องการลบ]
    D2 --> D3{ยืนยัน User\nถูกต้อง?}
    D3 -- ไม่ --> D2
    D3 -- ใช่ --> D4{User มี\nActive Resources?}
    D4 -- ใช่ --> D5[โอนย้าย / ปิด Resources\nก่อนลบ]
    D5 --> D6[ยืนยันการลบ User]
    D4 -- ไม่ --> D6
    D6 --> D7[กด Delete / Remove User]
    D7 --> D8{ลบสำเร็จ?}
    D8 -- ไม่ --> D9[ตรวจสอบ Error\nและแก้ไข]
    D9 --> D6
    D8 -- ใช่ --> D10[บันทึก Log\nการลบผู้ใช้งาน]
    D10 --> Z3([End - ลบสำเร็จ])

    %% ===== เพิ่มผู้ใช้งาน =====
    D -- เพิ่มผู้ใช้งาน --> A2[กรอกข้อมูล User ใหม่\nEmail / Username]
    A2 --> A3[กำหนด Role\nและ Permission]
    A3 --> A4{Role\nเหมาะสม?}
    A4 -- ไม่ --> A3
    A4 -- ใช่ --> A5[ส่ง Invitation\nหรือ Create Account]
    A5 --> A6{ส่งสำเร็จ?}
    A6 -- ไม่ --> A7[ตรวจสอบ Email\nและลองใหม่]
    A7 --> A5
    A6 -- ใช่ --> A8[แจ้ง User\nข้อมูล Login]
    A8 --> A9[บันทึก Log\nการเพิ่มผู้ใช้งาน]
    A9 --> Z4([End - เพิ่มสำเร็จ])

    %% Styling
    style A fill:#4CAF50,color:#fff
    style Z1 fill:#9E9E9E,color:#fff
    style Z2 fill:#2196F3,color:#fff
    style Z3 fill:#F44336,color:#fff
    style Z4 fill:#4CAF50,color:#fff
```

## ขั้นตอนสรุป

### 1. ตรวจสอบการใช้งาน (Check)
| ขั้นตอน | รายละเอียด |
|--------|-----------|
| 1 | Login Confluent Admin Console |
| 2 | ไปที่ User Management |
| 3 | ค้นหาและเลือก User |
| 4 | ตรวจสอบ Role, Permission และสถานะ |
| 5 | แก้ไขหากจำเป็น แล้วบันทึก |

### 2. ลบผู้ใช้งาน (Delete)
| ขั้นตอน | รายละเอียด |
|--------|-----------|
| 1 | ค้นหา User ที่ต้องการลบ |
| 2 | ตรวจสอบว่ามี Active Resources หรือไม่ |
| 3 | โอนย้าย/ปิด Resources (ถ้ามี) |
| 4 | ยืนยันและกด Delete |
| 5 | บันทึก Log การลบ |

### 3. เพิ่มผู้ใช้งาน (Add)
| ขั้นตอน | รายละเอียด |
|--------|-----------|
| 1 | กรอกข้อมูล User (Email/Username) |
| 2 | กำหนด Role และ Permission ที่เหมาะสม |
| 3 | ส่ง Invitation หรือสร้าง Account |
| 4 | แจ้ง Login credentials ให้ User |
| 5 | บันทึก Log การเพิ่มผู้ใช้งาน |

## หมายเหตุ
- ควร log ทุกการเปลี่ยนแปลงสิทธิ์เพื่อ audit trail
- การลบ User ควรได้รับการอนุมัติจาก Admin ก่อนเสมอ
- ตรวจสอบ Active Resources ก่อนลบเพื่อป้องกันข้อมูลสูญหาย
