# Skill Update FS · Codex local bridge

หน้าเว็บนี้ใช้ Codex CLI ที่ล็อกอินอยู่ในเครื่องเพื่ออัปเดต Financial HTML/Vue และ JavaScript ตามสกิล `ir-financial-html-updater` ที่ติดตั้งใน Codex ไม่ต้องมี API key และไม่มีช่อง prompt ให้กรอก

## สิ่งที่ต้องมี

- Windows, Node.js 18 ขึ้นไป และ Codex CLI ที่คำสั่ง `codex` เรียกได้จาก PowerShell
- ลงชื่อเข้าใช้ Codex CLI ด้วยบัญชี ChatGPT แล้ว (`codex login`)
- ติดตั้งสกิล `ir-financial-html-updater` ใน Codex เครื่องนั้น
- เปิดหน้าเว็บจาก `https://thanakon-kn.github.io/skill-update-fs/`

## เริ่มตัวเชื่อมบน Windows

1. ดาวน์โหลด `codex-bridge.mjs` จาก repository นี้ลงในเครื่อง
2. เปิด PowerShell ในโฟลเดอร์ที่ดาวน์โหลดไฟล์ แล้วรัน:

   ```powershell
   node .\codex-bridge.mjs
   ```

3. คัดลอกรหัสสุ่มที่แสดงในหน้าต่าง PowerShell
4. เปิดหน้าเว็บ ใส่รหัสนั้นในช่อง **เชื่อมต่อ Codex ในเครื่อง** แล้วกด **เชื่อมต่อ**
5. เลือกไฟล์และวางโค้ด เมื่อกดอัปเดต เว็บจะแสดงหน้าต่างยืนยันข้อมูลก่อนส่งให้ Codex
6. ปิดตัวเชื่อมด้วย `Ctrl+C` เมื่อใช้งานเสร็จ รหัสจะเปลี่ยนทุกครั้งที่เริ่มใหม่

หากเบราว์เซอร์ถามเรื่องการเข้าถึงเครือข่ายในเครื่อง ให้ตรวจว่าหน้าเว็บคือ `https://thanakon-kn.github.io/skill-update-fs/` ก่อนอนุญาต หน้าเว็บอื่นและเครื่องอื่นเชื่อมเข้าตัวช่วยนี้ไม่ได้ ตัวช่วย bind เฉพาะ `127.0.0.1` และตรวจ Origin ซ้ำทุกคำขอ

## ข้อมูลและการประมวลผล

- เบราว์เซอร์อ่านไฟล์ XLSX/CSV/TSV แล้วส่งข้อมูลตารางทุกชีตที่อ่านได้ พร้อมชื่อไฟล์ ภาษา โค้ด HTML/Vue และ JavaScript ไปยัง bridge ในเครื่อง
- ก่อนส่งแต่ละครั้ง ผู้ใช้ต้องยืนยันข้อมูลที่จะส่ง
- bridge เรียก Codex CLI ที่ลงชื่อเข้าใช้ไว้ โดยใช้สกิลในเครื่องและบัญชี ChatGPT นั้น ไม่มี API key ในเว็บหรือ repository
- Codex ส่งข้อมูลที่เลือกให้บริการโมเดล OpenAI เพื่อประมวลผลตามบัญชี ChatGPT
- Codex CLI ทำงานแบบ `read-only` และ `ephemeral`; bridge ลบไฟล์ schema/output ชั่วคราวเมื่อจบงาน
- bridge ไม่เปิดพอร์ตออกเครือข่าย ตัวเชื่อมรับคำขอจาก origin ของ GitHub Pages นี้เท่านั้น และมีรหัสสุ่มต่อการเริ่มหนึ่งครั้ง
- ตรวจผลลัพธ์และหมายเหตุในหน้าเว็บก่อนนำโค้ดไปใช้จริง

## แก้ปัญหา

- `codex` ไม่พบ: ตรวจว่า Codex CLI ใช้ได้ใน PowerShell ด้วย `codex --version` ก่อนเริ่ม bridge
- เข้า Codex ไม่ได้: ลงชื่อเข้าใช้ CLI ด้วย `codex login` แล้วเริ่ม bridge ใหม่
- เชื่อมต่อไม่ได้: ตรวจว่า PowerShell ที่รัน bridge ยังเปิดอยู่ และอนุญาต Local Network ให้หน้า GitHub Pages
- Codex ไม่พบสกิล: ติดตั้ง `ir-financial-html-updater` ใน Codex เครื่องนี้ก่อนใช้งาน

## ไฟล์

- `index.html`: หน้าเว็บ GitHub Pages
- `codex-bridge.mjs`: ตัวเชื่อม localhost เรียก Codex CLI
