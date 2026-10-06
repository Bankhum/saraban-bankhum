# ระบบสารบรรณ โรงเรียนบ้านคุ้ม (ประสาทราษฎร์วิทยา)

ระบบลงทะเบียนหนังสือรับ–ส่ง คำสั่ง ประกาศ บันทึกข้อความ เสนอผ่านรอง ผอ. ถึง ผอ. เกษียณและลงนามออนไลน์ มอบหมายงานตามกลุ่มงาน แจ้งเตือนผ่าน LINE OA ทำงานบน Cloudflare Workers ไฟล์เดียว (`worker.js`)

## ติดตั้งบน Cloudflare (ไม่ต้องใช้คำสั่ง)

1. Workers & Pages → Create application → Start with Hello World → ตั้งชื่อ `saraban-bankhum` → Deploy
2. Edit code → ลบโค้ดเดิม → วางเนื้อหา `worker.js` ทั้งไฟล์ → Deploy
3. Storage & databases → D1 → Create database ชื่อ `saraban-bankhum`
4. Storage & databases → R2 → Create bucket ชื่อ `saraban-bankhum-files`
5. Worker → Settings → Bindings → Add
   - D1 database ตัวแปรชื่อ `DB` → เลือก `saraban-bankhum`
   - R2 bucket ตัวแปรชื่อ `FILES` → เลือก `saraban-bankhum-files`
6. เปิดลิงก์ `https://saraban-bankhum.<subdomain>.workers.dev` → สร้างบัญชีผู้อำนวยการ (บัญชีแรก) → เพิ่มบัญชีบุคลากรที่หน้า ตั้งค่า

ตารางในฐานข้อมูลสร้างอัตโนมัติเมื่อเปิดระบบครั้งแรก

## LINE OA (ไม่บังคับ)

- Worker → Settings → Variables and Secrets → เพิ่มแบบ **Secret**
  - `LINE_CHANNEL_SECRET`
  - `LINE_CHANNEL_ACCESS_TOKEN`
- LINE Developers → Messaging API → Webhook URL: `https://<โดเมนระบบ>/line/webhook` → เปิด Use webhook
- เชิญ OA เข้ากลุ่มครู แล้วพิมพ์ `เชื่อมกลุ่มสารบรรณ`
- บุคลากรผูกบัญชี: ระบบ → ตั้งค่า → รับรหัสผูก LINE → พิมพ์ `ผูก 123456` ในแชต OA

## สรุปงานตอนเช้า (ไม่บังคับ)

Worker → Settings → Trigger events → Cron `0 0 * * 1-5` (07.00 น. จันทร์–ศุกร์)

## อัปเดตระบบ

วาง `worker.js` เวอร์ชันใหม่ทับใน Edit code แล้วกด Deploy ข้อมูลในฐานข้อมูลไม่หาย

> ห้ามใส่รหัส LINE หรือรหัสผ่านใด ๆ ไว้ใน repository นี้ ให้เก็บเป็น Secret ใน Cloudflare เท่านั้น
