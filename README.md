# Linux-Postman-Installation
# วิธีติดตั้ง Postman บน Linux (Manual Installation)

การติดตั้งด้วยวิธีนี้จะช่วยแก้ปัญหาเรื่อง Permission (EACCES) เวลาที่ Postman (แบบ Snap) พยายามเข้าถึงไฟล์ในเครื่อง เช่น Python venv หรือ Local files อื่นๆ

## 1. ดาวน์โหลดโปรแกรม
ไปที่เว็บไซต์ [Postman Download Page](https://www.postman.com/downloads/) แล้วคลิกดาวน์โหลดเวอร์ชัน **Linux (x64)**
*   จะได้ไฟล์ชื่อประมาณ `postman-linux-x64.tar.gz`

## 2. แตกไฟล์และติดตั้ง
เปิด Terminal แล้วรันคำสั่งตามลำดับดังนี้:

1.  **ไปที่โฟลเดอร์ที่ดาวน์โหลดไฟล์มา** (ปกติคือ Downloads)
    ```bash
    cd ~/Downloads
    ```

2.  **แตกไฟล์**
    ```bash
    tar -xzf postman-linux-x64.tar.gz
    ```

3.  **ย้ายไปไว้ที่ `/opt`** (เพื่อให้เป็นระเบียบและใช้ร่วมกันได้ทุกคนในเครื่อง)
    - *ถ้ามี folder เก่าอยู่แล้ว ให้ลบอออกก่อน*
    ```bash
    sudo rm -rf /opt/Postman
    sudo mv Postman /opt/
    ```

4.  **สร้าง Link เรียกใช้งาน** (เพื่อให้พิมพ์คำว่า `postman` ใน terminal ได้เลย)
    ```bash
    sudo ln -sf /opt/Postman/Postman /usr/local/bin/postman
    ```

## 3. สร้าง Icon บนเมนู (Desktop Entry)
เพื่อให้สามารถค้นหาและกดเปิดจาก Application Menu ได้ ให้สร้างไฟล์ Desktop launcher

1.  **สร้างไฟล์** `postman.desktop`
    ```bash
    nano ~/.local/share/applications/postman.desktop
    ```

2.  **วางเนื้อหาข้างล่างนี้ลงไป**
    ```ini
    [Desktop Entry]
    Encoding=UTF-8
    Name=Postman
    Exec=postman
    Icon=/opt/Postman/app/resources/app/assets/icon.png
    Terminal=false
    Type=Application
    Categories=Development;
    ```

3.  **บันทึกไฟล์** (กด `Ctrl+O` -> `Enter` -> `Ctrl+X`)

## 4. ทดสอบใช้งาน
*   **เปิดผ่าน Terminal**: พิมพ์ `postman` แล้ว Enter
*   **เปิดผ่าน Menu**: กดปุ่ม Super (Windows) แล้วพิมพ์ค้นหา "Postman"

---
**หมายเหตุ:** วิธีนี้ Postman จะทำงานแบบไม่มี Sandbox มาขวาง ทำให้สามารถเชื่อมต่อกับ **MCP Server** ที่รันผ่าน Python venv (`.venv` หรือ `.local`) ได้โดยไม่ติดปัญหา Permission ครับ
