# Week 6: N-Tier Architecture with Redis Caching & Load Balancing

**จัดทำโดย:** ธนมินทร์ เปลี่ยนพร้อม  
**เลขประจำตัว:** 67543210032-8

---

## 📋 สรุปและเปรียบเทียบระบบ

ตารางเปรียบเทียบความแตกต่างระหว่างการออกแบบระบบในสัปดาห์ที่ 6 แบบพื้นฐาน กับโปรเจกต์ระดับ Advanced (Term Project)

| คุณสมบัติ | Week 6 เดิม (Basic Docker) | Term Project Week 6 (Advanced) |
| :--- | :--- | :--- |
| **จำนวน Container** | 3 (Nginx, API, DB) | 6 (3 App + DB + Redis + Nginx) |
| **App Instances** | 1 Instance | 3 Instances (Scalable) |
| **ระบบ Cache** | ❌ ไม่มี | ✅ Redis (TTL-based) |
| **Load Balancing** | ❌ ไม่มี | ✅ Nginx (Round-Robin) |
| **Health Check** | Basic | ✅ แสดง Instance ID + Cache Stats |
| **Scaling** | ❌ ทำไม่ได้ | ✅ `docker compose --scale app=3` |
| **Fault Tolerance** | ❌ ต่ำ (ถ้า API ล่ม = ระบบหยุดทำงาน) | ✅ สูง (Redundancy ผ่าน Multi-instance) |

### 📊 Quality Attributes Score
* **Performance:** * เดิม: ★★☆☆☆ | ใหม่: ★★★★☆ (ด้วยการใช้ Cache)
* **Scalability:** * เดิม: ★☆☆☆☆ | ใหม่: ★★★★☆ (รองรับ Multi-Instance)
* **Availability:** * เดิม: ★★☆☆☆ | ใหม่: ★★★★☆ (มีระบบสำรองเมื่อ Instance อื่นล่ม)

---

## 🏆 Challenge: แนวทางการพัฒนาต่อ

| ระดับ | ภารกิจ (Challenge) | คำแนะนำ |
| :---: | :--- | :--- |
| ⭐ | เพิ่ม Cache สำหรับ `GET /tasks/:id` | ดูตัวอย่าง `getTaskById` ใน Service Layer |
| ⭐⭐ | เพิ่ม `X-Cache-Status` Header | เพิ่ม Middleware เพื่อเช็คว่าสถานะเป็น HIT หรือ MISS ใน Response |
| ⭐⭐⭐ | เปลี่ยน Load Balancing Algorithm | ศึกษาการใช้ `least_conn` แทน Round-Robin ใน Nginx Upstream |

---

## 📤 การส่งงานทาง Git

```bash
# เข้าสู่ Folder โปรเจกต์
cd ~/term-project/week6-ntier-redis

# ตรวจสอบความเรียบร้อย
git status

# Stage และ Commit พร้อมข้อความอธิบาย
git add -A
git commit -m "Week 6: N-Tier Architecture with Redis Caching + Load Balancing
- Added Redis caching layer (Cache-Aside pattern)
- Configured Nginx load balancing (Round-Robin, 3 instances)
- Health check endpoint with instance ID + cache stats
- Docker Compose with --scale support
- Load testing shows improved response times"

# Push ไปยัง Repository
git push origin main

✅ Deliverables Checklist
[x] docker-compose.yml: รองรับการรัน docker compose up --scale app=3

[x] Redis Caching: ทำงานได้จริง (ตรวจสอบผ่าน HIT/MISS ใน logs)

[x] Load Balancing: ทำงานได้จริง (Instance ID สลับกันเมื่อ Refresh)

[x] Frontend: แสดงผล Task Board พร้อมข้อมูล Instance Info

[x] Health Check: Endpoint แสดงสถิติของ Cache ได้ถูกต้อง

[x] Git History: Commit message ชัดเจนและอธิบายสิ่งที่ทำได้ครบถ้วน
