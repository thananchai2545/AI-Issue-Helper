# {ชื่อโปรเจกต์}

## ภาพรวมโปรเจกต์

{อธิบายว่าโปรเจกต์นี้ทำอะไร ใช้สำหรับแก้ปัญหาอะไร เช่น เป็นระบบ API สำหรับจัดการข้อมูลลูกค้า หรือ แอปพลิเคชันเว็บสำหรับแสดงผลแดชบอร์ด ฯลฯ}

**คำแนะนำ:** กรุณาแก้ไขส่วนนี้ให้ตรงกับวัตถุประสงค์ของโปรเจกต์

## Tech Stack

- **Backend:** Node.js, Express (ถ้ามี)
- **Frontend:** React / Next.js / Vue (ตามที่พบใน package.json)
- **ภาษา:** TypeScript / JavaScript
- **ฐานข้อมูล:** PostgreSQL / MySQL / SQLite (ดูใน schema.prisma หรือ config)
- **ORM:** Prisma / Sequelize / TypeORM
- **Containerization:** Docker, Docker Compose (ถ้ามีไฟล์ docker-compose.yml)
- **อื่น ๆ :** {เพิ่มตามที่พบใน project เช่น Redis, Nginx, etc.}

## Project Structure

```
.
├── src/
│   ├── modules/         # โมดูลต่าง ๆ (เช่น users, products)
│   ├── common/          # middleware, utils, helpers
│   ├── config/          # ไฟล์ตั้งค่า
│   └── app.ts           # จุดเริ่มต้นของแอป
├── prisma/
│   ├── schema.prisma    # schema ฐานข้อมูล
│   └── seed.ts          # ข้อมูลเริ่มต้น
├── docker-compose.yml   # (ถ้ามี)
├── Dockerfile           # (ถ้ามี)
├── .env.example         # ตัวอย่างตัวแปรแวดล้อม
├── package.json
└── README.md
```

**หมายเหตุ:** โครงสร้างจริงอาจแตกต่าง โปรดตรวจสอบใน repository

## Requirements

สิ่งที่ต้องติดตั้งก่อนเริ่ม:

- **Node.js** เวอร์ชัน {ดูใน .nvmrc หรือ engines ใน package.json}
- **npm** หรือ **yarn** (ตามที่ใช้)
- **Docker** และ **Docker Compose** (ถ้าจะรันด้วย container)
- **ฐานข้อมูล** (ถ้าไม่ได้ใช้ Docker) เช่น PostgreSQL, MySQL ตามที่กำหนด

## Environment Variables

คัดลอกไฟล์ `.env.example` ไปเป็น `.env` แล้วแก้ไขค่าตามต้องการ

```bash
cp .env.example .env
```

| ตัวแปร | คำอธิบาย | ค่าเริ่มต้น / ตัวอย่าง |
|--------|----------|----------------------|
| `DATABASE_URL` | URL สำหรับเชื่อมต่อฐานข้อมูล | `postgresql://user:password@localhost:5432/dbname` |
| `PORT` | พอร์ตที่แอปจะรัน | `3000` |
| `JWT_SECRET` | Secret key สำหรับ JWT | `your-secret-key` |
| `NODE_ENV` | โหมดการทำงาน | `development` / `production` |
| {เพิ่มตามไฟล์ .env.example} | ... | ... |

**หมายเหตุ:** ตรวจสอบไฟล์ `.env.example` ในโปรเจกต์เพื่อดูรายการตัวแปรทั้งหมด

## Installation

ติดตั้ง dependencies:

```bash
npm install
# หรือถ้าใช้ yarn:
yarn install
```

## Development

รันแอปในโหมดพัฒนา:

```bash
npm run dev
# หรือ
yarn dev
```

ถ้ามี frontend และ backend แยกกัน ให้เปิด terminal แยกหรือใช้คำสั่ง concurrently (ดูใน `scripts` ของ package.json)

## Build

สร้าง production build:

```bash
npm run build
# หรือ
yarn build
```

ผลลัพธ์จะอยู่ในโฟลเดอร์ `dist/` หรือ `build/` (ตามที่กำหนดใน tsconfig หรือ webpack)

## Database Setup

### Prisma (ถ้าใช้)

#### Migrate database

```bash
npx prisma migrate dev --name init
```

#### Generate Prisma Client

```bash
npx prisma generate
```

#### Seed data (ถ้ามี)

```bash
npm run seed
# หรือ
npx prisma db seed
```

**หมายเหตุ:** ถ้าใช้ ORM อื่น (Sequelize, TypeORM) ให้ปรับคำสั่งตามนั้น ดูรายละเอียดจากไฟล์ `package.json` script หรือ docs ของ ORM

## API Endpoints

(รายการ endpoint หลัก – ตรวจสอบเพิ่มเติมจากไฟล์ routes หรือ controller)

| Method | Endpoint | คำอธิบาย |
|--------|----------|----------|
| GET | `/api/users` | ดึงรายการผู้ใช้ทั้งหมด |
| POST | `/api/users` | สร้างผู้ใช้ใหม่ |
| GET | `/api/users/:id` | ดึงผู้ใช้ตาม ID |
| PUT | `/api/users/:id` | อัปเดตผู้ใช้ |
| DELETE | `/api/users/:id` | ลบผู้ใช้ |
| POST | `/api/auth/login` | เข้าสู่ระบบ |
| ... | ... | ... |

**หมายเหตุ:** รายการ endpoint จริงขึ้นอยู่กับโค้ดในโปรเจกต์ ควรตรวจสอบในไฟล์ route หรือ controller

## Docker Usage

ถ้ามีไฟล์ `docker-compose.yml`:

```bash
# รัน services ทั้งหมด (db, app, etc.)
docker-compose up -d

# หยุด services
docker-compose down
```

ถ้าต้องการ build image และรันเฉพาะแอป:

```bash
docker build -t my-app .
docker run -p 3000:3000 --env-file .env my-app
```

**หมายเหตุ:** ถ้าไม่มี Docker หรือ docker-compose ให้ข้ามส่วนนี้

## CI/CD

ถ้ามี GitHub Actions หรือ CI อื่น:
- เมื่อ merge ไปยัง branch `dev` → deploy ไปยัง staging
- เมื่อ merge ไปยัง `main` หรือ `master` → deploy ไปยัง production

ดูรายละเอียดใน `.github/workflows/`

## Deployment

### Staging

1. checkout branch `dev`
2. รัน `npm run build`
3. deploy ไปยัง environment staging (เช่น VPS, Heroku, AWS)

### Production

1. checkout branch `main`
2. รัน `npm run build`
3. deploy ไปยัง production environment

**หมายเหตุ:** ขั้นตอนจริงอาจแตกต่าง ดูในไฟล์ deployment config หรือ CI/CD workflow

## Troubleshooting

- **พอร์ตถูกใช้แล้ว** – เปลี่ยน `PORT` ใน `.env` หรือหยุด process ที่ใช้พอร์ตนั้น
- **เชื่อมต่อฐานข้อมูลไม่ได้** – ตรวจสอบ `DATABASE_URL` และตรวจสอบว่าฐานข้อมูลกำลังรันอยู่
- **Prisma error** – รัน `npx prisma generate` ใหม่ หรือตรวจสอบ schema
- **Dependency ขาด** – ลบ `node_modules` และ `package-lock.json` แล้ว `npm install` ใหม่
- **ไฟล์ .env ไม่พบ** – คัดลอกจาก `.env.example` แล้วกรอกค่าที่ถูกต้อง

## Notes

- ตรวจสอบไฟล์ `package.json` สำหรับ scripts ทั้งหมดที่ใช้ได้
- ถ้ามีไฟล์ `.nvmrc` ให้ใช้ Node.js เวอร์ชันที่ระบุ
- การตั้งค่าเพิ่มเติม (เช่น CORS, rate limit) ดูในไฟล์ config
- สำหรับ developer ใหม่: ให้อ่านเอกสารเพิ่มเติมจาก comments ในโค้ด
- หากพบปัญหาหรือข้อสงสัย ให้เปิด issue ใน repository