sequenceDiagram
    participant User
    participant Web Browser
    participant Application Server
    participant Database

    group สมัครสมาชิก
        User->>Web Browser: กรอกข้อมูลสมัครสมาชิก
        activate Web Browser
        Web Browser->>Application Server: ส่งข้อมูลสมัครสมาชิก
        activate Application Server
        Application Server->>Database: ตรวจสอบข้อมูลซ้ำ
        activate Database
        Database-->>Application Server: ผลการตรวจสอบ
        deactivate Database
        alt ข้อมูลไม่ซ้ำ
            Application Server->>Database: บันทึกข้อมูลสมาชิกใหม่
            activate Database
            Database-->>Application Server: ยืนยันการบันทึก
            deactivate Database
            Application Server-->>Web Browser: สำเร็จ
            deactivate Application Server
            Web Browser-->>User: แสดงข้อความสำเร็จ
            deactivate Web Browser
        else ข้อมูลซ้ำ
            Application Server-->>Web Browser: แจ้งข้อผิดพลาด
            deactivate Application Server
            Web Browser-->>User: แสดงข้อความผิดพลาด
            deactivate Web Browser
        end
    end

    group ล็อกอิน
        User->>Web Browser: กรอกข้อมูลล็อกอิน
        activate Web Browser
        Web Browser->>Application Server: ส่งข้อมูลล็อกอิน
        activate Application Server
        Application Server->>Database: ตรวจสอบข้อมูลผู้ใช้
        activate Database
        Database-->>Application Server: ผลการตรวจสอบ
        deactivate Database
        alt ข้อมูลถูกต้อง
            Application Server->>Web Browser: สร้าง Session
            deactivate Application Server
            Web Browser-->>User: เข้าสู่ระบบสำเร็จ
            deactivate Web Browser
        else ข้อมูลไม่ถูกต้อง
            Application Server-->>Web Browser: แจ้งข้อผิดพลาด
            deactivate Application Server
            Web Browser-->>User: แสดงข้อความผิดพลาด
            deactivate Web Browser
        end
    end
