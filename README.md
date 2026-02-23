Part 6: สรุปและเปรียบเทียบ
เปรียบเทียบ Week 6 เดิม vs Term Project Week 6
┌─────────────────────────────────────────────────────────────────────────────┐
│  Week 6 เดิม (Basic Docker)          Term Project Week 6 (Advanced)          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Containers: 3                       Containers: 6 (3 app + db + redis +    │
│  • nginx + api + db                  nginx)                                 │
│                                                                             │
│  App Instances: 1                    App Instances: 3 (scalable)            │
│  Cache: ❌ ไม่มี                       Cache: ✅ Redis (TTL-based)            │
│  Load Balancing: ❌                  Load Balancing: ✅ Nginx Round-Robin   │
│  Health Check: Basic                 Health Check: ✅ แสดง Instance ID +    │
│                                      Cache Stats                            │
│                                                                             │
│  Scaling: ❌ ทำไม่ได้                  Scaling: ✅ docker compose --scale     │
│  Fault Tolerance: ❌ ถ้า API ล่ม=จบ    Fault Tolerance: ✅ ยังมี instance อื่น    │
│                                                                             │
│  Quality Attributes:                 Quality Attributes:                    │
│  Performance:  ★★☆☆☆                 Performance: ★★★★☆ (Cache)             │
│  Scalability:  ★☆☆☆☆                 Scalability: ★★★★☆ (Multi-Instance)    │
│  Availability: ★★☆☆☆                 Availability: ★★★★☆ (Redundancy)       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
🏆 Challenge: ทำต่อเอง
ระดับ	Challenge	คำแนะนำ
⭐	เพิ่ม cache สำหรับ GET /tasks/:id	ดูตัวอย่าง getTaskById ใน Service Layer
⭐⭐	เพิ่ม X-Cache-Status header (HIT/MISS) ใน response	เพิ่ม middleware ที่เช็ค cache ก่อน
⭐⭐⭐	เปลี่ยน Load Balancing เป็น Least Connections	ศึกษา least_conn ใน nginx upstream
📤 การส่งงานทาง Git
cd ~/term-project/week6-ntier-redis

# ตรวจสอบไฟล์
git status

# Commit
git add -A
git commit -m "Week 6: N-Tier Architecture with Redis Caching + Load Balancing

- Added Redis caching layer (Cache-Aside pattern)
- Configured Nginx load balancing (Round-Robin, 3 instances)
- Health check endpoint with instance ID + cache stats
- Docker Compose with --scale support
- Load testing shows improved response times"

# Push
git push origin main
Deliverables Checklist
✅	รายการ
☐	docker-compose.yml ที่รัน docker compose up --scale app=3 ได้
☐	Redis caching ทำงาน (เห็น HIT/MISS ใน logs)
☐	Load Balancing ทำงาน (Instance ID สลับกัน)
☐	Frontend แสดง Task Board + Instance Info
☐	Health Check endpoint แสดง Cache Stats
☐	Git commit พร้อม message อธิบาย

