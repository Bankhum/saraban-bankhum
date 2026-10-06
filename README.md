# E-Sarabun Bankhum · ระบบสารบรรณอิเล็กทรอนิกส์ โรงเรียนบ้านคุ้ม (ประสารราษฎร์วิทยา)

ระบบลงทะเบียนหนังสือรับ–ส่ง คำสั่ง ประกาศ บันทึกข้อความ เสนอผ่านรอง ผอ. ถึง ผอ. เกษียณและลงนามบน PDF มอบหมายงานตามกลุ่มงาน ติดตามการรับทราบ และแจ้งเตือนผ่าน LINE OA
ทำงานบน Cloudflare Workers ไฟล์เดียว (`worker.js`) เก็บข้อมูลและไฟล์แนบในฐานข้อมูล D1

พัฒนาโดย ครูดีลาภ ปราบสงบ ครูชำนาญการพิเศษ โรงเรียนบ้านคุ้ม (ประสารราษฎร์วิทยา)

## อัปเดตระบบ

Cloudflare → Workers & Pages → `saraban-bankhum` → Edit code → ลบโค้ดเดิม → วาง `worker.js` ทั้งไฟล์ → Deploy
ข้อมูลในฐานข้อมูลไม่หาย

## ติดตั้งใหม่ (กรณีย้ายบัญชี)

1. Workers & Pages → Create → Hello World → ตั้งชื่อ `saraban-bankhum` → Deploy
2. Edit code → วาง `worker.js` → Deploy
3. Storage & databases → D1 → Create database ชื่อ `saraban-bankhum`
4. Worker → Settings → Bindings → Add → D1 database ตัวแปร `DB` → เลือก `saraban-bankhum`
5. เปิดลิงก์ของ Worker → สร้างบัญชีผู้ดูแลบัญชีแรก

ตารางในฐานข้อมูลสร้างอัตโนมัติเมื่อเปิดระบบครั้งแรก (ไม่ต้องใช้ R2)

## LINE OA

- Worker → Settings → Variables and Secrets → เพิ่มแบบ **Secret**: `LINE_CHANNEL_SECRET`, `LINE_CHANNEL_ACCESS_TOKEN`
- LINE Developers → Messaging API → Webhook URL `https://<โดเมนระบบ>/line/webhook` → เปิด Use webhook → Verify
- LINE OA Manager → ตั้งค่าการตอบกลับ: ปิดแชท, เปิด Webhook, ปิดข้อความตอบกลับอัตโนมัติ
- เชิญ OA เข้ากลุ่มครู แล้วพิมพ์ในกลุ่ม `เชื่อมกลุ่มสารบรรณ`
- ครูผูกบัญชี: ระบบ → ตั้งค่า → รับรหัสผูก LINE → พิมพ์ `ผูก 123456` ในแชต OA

## สรุปงานตอนเช้า

Worker → Settings → Trigger events → Cron `0 0 * * MON-FRI` (07.00 น. จันทร์–ศุกร์ เวลาไทย)

> ห้ามใส่รหัส LINE หรือรหัสผ่านใด ๆ ไว้ใน repository นี้ ให้เก็บเป็น Secret ใน Cloudflare เท่านั้น
