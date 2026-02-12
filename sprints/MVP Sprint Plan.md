# 🏃 SanakIT MVP Sprint Plan

## 🎯 MVP Vision
Membuat platform community + AI mentor sederhana yang **bisa digunakan** oleh mahasiswa IT.

**MVP = Minimum Viable Product** → Fitur paling inti yang bisa memberikan value ke user.

> [!NOTE]
> MVP bukan versi final. Tujuannya adalah validasi ide secepat mungkin dengan effort minimal.

---

## 📅 Sprint Overview

| Sprint | Durasi | Focus | Complexity |
|--------|--------|-------|------------|
| Sprint 1 | 1 minggu | Project Setup & Foundation | ⭐ Low |
| Sprint 2 | 1-2 minggu | Authentication System | ⭐⭐ Medium |
| Sprint 3 | 2 minggu | Community System (Core MVP) | ⭐⭐⭐ Medium-High |
| Sprint 4 | 2 minggu | AI Mentor Integration | ⭐⭐⭐ Medium-High |
| Sprint 5 | 1-2 minggu | Portfolio & Career Prep | ⭐⭐ Medium |

**Total Estimasi: 7-9 minggu**

---

## 🏗 Sprint 1: Project Setup & Foundation

### 🎯 Goal
Setup project Next.js dengan struktur folder yang benar, konfigurasi tools, dan landing page.

### 📦 Task Breakdown

| Task | Detail | Learning Focus |
|------|--------|---------------|
| Init Next.js + TypeScript | `npx create-next-app` | Project scaffolding |
| Setup Tailwind + ShadCN | Config styling system | CSS framework integration |
| Setup Prisma + PostgreSQL | Database connection | ORM setup |
| Setup folder structure | Feature-based folders | Clean architecture |
| Create landing page | Hero, Features, CTA | Component composition |
| Setup ESLint + Prettier | Code quality tools | Code consistency |
| Git init + first commit | Version control | Git workflow |

### 🧠 Yang Akan Dipelajari
- Next.js App Router architecture
- TypeScript basics untuk React
- Prisma ORM setup & configuration
- Component-based thinking

### 🧪 Testing Plan
- [ ] `npm run build` — no error
- [ ] Landing page tampil di `localhost:3000`
- [ ] Prisma connected ke database
- [ ] ESLint & Prettier berjalan

### 📌 Deliverable
- ✅ Project running di localhost
- ✅ Landing page responsive
- ✅ Database connected
- ✅ Clean folder structure

---

## 🏗 Sprint 2: Authentication System

### 🎯 Goal
User bisa register, login, dan melihat profile.

### 👤 User Stories
```
Sebagai mahasiswa IT
Saya ingin mendaftar akun
Agar saya bisa mengakses fitur community
```

### 📦 Task Breakdown

| Task | Detail | Learning Focus |
|------|--------|---------------|
| Setup NextAuth.js | Auth provider | Authentication flow |
| Database schema: User | Prisma model | Database modeling |
| Register page | Form + validation | Form handling |
| Login page | Email/Password | Auth flow |
| Profile page | User info display | Protected routes |
| Auth middleware | Route protection | Middleware pattern |
| Session management | JWT/Session | Security basics |

### 🗄 Database Schema Preview
```prisma
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String
  password  String
  avatar    String?
  bio       String?
  role      Role     @default(MEMBER)
  createdAt DateTime @default(now()) @map("created_at")
  updatedAt DateTime @updatedAt @map("updated_at")

  @@map("users")
}

enum Role {
  MEMBER
  MENTOR
  ADMIN
}
```

### 🧠 Yang Akan Dipelajari
- Authentication vs Authorization
- Hashing password (bcrypt)
- JWT & Session management
- Protected routes di Next.js
- Zod validation
- React Hook Form

### 🧪 Testing Plan
- [ ] Register berhasil → data masuk database
- [ ] Login berhasil → redirect ke dashboard
- [ ] Route protected → redirect ke login jika belum auth
- [ ] Invalid input → menampilkan error validation

### 📌 Deliverable
- ✅ User bisa register & login
- ✅ Profile page menampilkan data user
- ✅ Routes terproteksi

---

## 🏗 Sprint 3: Community System (Core MVP)

### 🎯 Goal
User bisa membuat post, like, dan comment di community.

### 👤 User Stories
```
Sebagai mahasiswa IT
Saya ingin membagikan pengalaman belajar
Agar sesama mahasiswa bisa berdiskusi
```

### 📦 Task Breakdown

| Task | Detail | Learning Focus |
|------|--------|---------------|
| Database schema: Post, Comment, Like | Prisma relations | Database relationships |
| Create post (CRUD) | Form + API | REST API design |
| Feed page | List posts | Data fetching (TanStack Query) |
| Like system | Toggle like | Optimistic update |
| Comment system | Nested comments | Recursive component |
| Post detail page | Single post view | Dynamic routes |
| API routes | REST endpoints | API architecture |

### 🗄 Database Schema Preview
```prisma
model Post {
  id        String    @id @default(cuid())
  title     String
  content   String
  authorId  String    @map("author_id")
  author    User      @relation(fields: [authorId], references: [id])
  likes     Like[]
  comments  Comment[]
  tags      String[]
  status    PostStatus @default(PUBLISHED)
  createdAt DateTime  @default(now()) @map("created_at")
  updatedAt DateTime  @updatedAt @map("updated_at")

  @@map("community_posts")
}

model Comment {
  id        String   @id @default(cuid())
  content   String
  authorId  String   @map("author_id")
  author    User     @relation(fields: [authorId], references: [id])
  postId    String   @map("post_id")
  post      Post     @relation(fields: [postId], references: [id])
  createdAt DateTime @default(now()) @map("created_at")

  @@map("comments")
}

model Like {
  id        String   @id @default(cuid())
  userId    String   @map("user_id")
  user      User     @relation(fields: [userId], references: [id])
  postId    String   @map("post_id")
  post      Post     @relation(fields: [postId], references: [id])
  createdAt DateTime @default(now()) @map("created_at")

  @@unique([userId, postId])
  @@map("likes")
}
```

### 🧠 Yang Akan Dipelajari
- Database relationships (1:N, N:M)
- REST API best practices
- TanStack Query (React Query) — client-server state
- Optimistic updates
- Pagination
- Server Components vs Client Components

### 🧪 Testing Plan
- [ ] CRUD post berfungsi
- [ ] Like toggle works (1 user = 1 like per post)
- [ ] Comments muncul di post detail
- [ ] Feed menampilkan posts terbaru
- [ ] Pagination berfungsi

### 📌 Deliverable
- ✅ Community feed berfungsi
- ✅ User bisa create, read, update, delete post
- ✅ Like & comment system berjalan

---

## 🏗 Sprint 4: AI Mentor Integration

### 🎯 Goal
User bisa chat dengan AI Mentor untuk tanya materi IT & career advice.

### 👤 User Stories
```
Sebagai mahasiswa IT
Saya ingin bertanya tentang materi programming
Agar saya mendapat jawaban yang relevan & edukatif
```

### 📦 Task Breakdown

| Task | Detail | Learning Focus |
|------|--------|---------------|
| Database schema: MentorSession, Message | Chat history | Data modeling |
| OpenAI API integration | LLM provider | API integration |
| Chat UI | Message interface | Real-time UI |
| Streaming response | Server-Sent Events | Streaming pattern |
| System prompt engineering | AI behavior | Prompt design |
| Chat history | Save & load | Data persistence |
| Rate limiting | Usage control | Security |

### 🗄 Database Schema Preview
```prisma
model MentorSession {
  id        String    @id @default(cuid())
  title     String?
  userId    String    @map("user_id")
  user      User      @relation(fields: [userId], references: [id])
  messages  Message[]
  createdAt DateTime  @default(now()) @map("created_at")
  updatedAt DateTime  @updatedAt @map("updated_at")

  @@map("mentor_sessions")
}

model Message {
  id        String      @id @default(cuid())
  role      MessageRole
  content   String
  sessionId String      @map("session_id")
  session   MentorSession @relation(fields: [sessionId], references: [id])
  createdAt DateTime    @default(now()) @map("created_at")

  @@map("messages")
}

enum MessageRole {
  USER
  ASSISTANT
  SYSTEM
}
```

### 🧠 Yang Akan Dipelajari
- OpenAI API integration
- Streaming response (SSE / ReadableStream)
- Chat UI architecture
- Prompt engineering
- Rate limiting strategy
- Environment variable management

### 🧪 Testing Plan
- [ ] Chat mengirim pesan ke AI & mendapat response
- [ ] Streaming response tampil bertahap
- [ ] Chat history tersimpan
- [ ] Session bisa di-load kembali
- [ ] Rate limiting berfungsi

### 📌 Deliverable
- ✅ AI Mentor chatbot berfungsi
- ✅ Chat history tersimpan
- ✅ Streaming response

---

## 🏗 Sprint 5: Portfolio & Career Prep

### 🎯 Goal
User bisa menampilkan portfolio project dan tracking career progress.

### 👤 User Stories
```
Sebagai mahasiswa IT
Saya ingin menampilkan project saya
Agar bisa dilihat oleh recruiter & sesama mahasiswa
```

### 📦 Task Breakdown

| Task | Detail | Learning Focus |
|------|--------|---------------|
| Database schema: Project, CareerProgress | Portfolio data | Schema design |
| Project showcase page | Display projects | Gallery/Grid layout |
| Add/Edit project form | CRUD project | Form + file upload |
| Career progress tracker | Skill tracking | Progress visualization |
| Public profile page | Portfolio view | SEO optimization |
| Learning path display | Roadmap visual | Data visualization |

### 🗄 Database Schema Preview
```prisma
model Project {
  id          String   @id @default(cuid())
  title       String
  description String
  techStack   String[]  @map("tech_stack")
  githubUrl   String?   @map("github_url")
  liveUrl     String?   @map("live_url")
  imageUrl    String?   @map("image_url")
  authorId    String    @map("author_id")
  author      User      @relation(fields: [authorId], references: [id])
  createdAt   DateTime  @default(now()) @map("created_at")
  updatedAt   DateTime  @updatedAt @map("updated_at")

  @@map("projects")
}

model CareerProgress {
  id        String   @id @default(cuid())
  userId    String   @map("user_id")
  user      User     @relation(fields: [userId], references: [id])
  skill     String
  level     SkillLevel @default(BEGINNER)
  notes     String?
  createdAt DateTime @default(now()) @map("created_at")
  updatedAt DateTime @updatedAt @map("updated_at")

  @@map("career_progress")
}

enum SkillLevel {
  BEGINNER
  INTERMEDIATE
  ADVANCED
  EXPERT
}
```

### 🧠 Yang Akan Dipelajari
- File upload handling
- Image optimization (Next.js Image)
- SEO best practices
- Public vs Private routes
- Data visualization basics

### 🧪 Testing Plan
- [ ] CRUD project berfungsi
- [ ] Portfolio page menampilkan semua project
- [ ] Public profile accessible tanpa login
- [ ] Career progress tracking works

### 📌 Deliverable
- ✅ Portfolio showcase berfungsi
- ✅ Career progress tracker
- ✅ Public profile page

---

## 🧭 Architecture Overview (MVP)

```
sanakIT/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── (auth)/             # Auth pages group
│   │   │   ├── login/
│   │   │   └── register/
│   │   ├── (dashboard)/        # Protected pages
│   │   │   ├── community/
│   │   │   ├── mentor/
│   │   │   ├── portfolio/
│   │   │   └── profile/
│   │   ├── api/                # API Routes
│   │   │   ├── auth/
│   │   │   ├── posts/
│   │   │   ├── mentor/
│   │   │   └── projects/
│   │   ├── layout.tsx
│   │   └── page.tsx            # Landing page
│   ├── components/             # Reusable components
│   │   ├── ui/                 # ShadCN components
│   │   ├── layout/             # Header, Footer, Sidebar
│   │   └── shared/             # Common components
│   ├── features/               # Feature modules
│   │   ├── auth/
│   │   ├── community/
│   │   ├── mentor/
│   │   └── portfolio/
│   ├── lib/                    # Utilities
│   │   ├── prisma.ts           # Prisma client
│   │   ├── auth.ts             # Auth config
│   │   └── utils.ts            # Helper functions
│   ├── hooks/                  # Custom React hooks
│   ├── services/               # API service layer
│   └── types/                  # TypeScript types
├── prisma/
│   └── schema.prisma           # Database schema
├── public/                     # Static assets
├── .env                        # Environment variables
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## 📊 Tech Stack Summary (MVP)

| Layer | Technology | Kenapa? |
|-------|-----------|---------|
| Framework | Next.js 15 (App Router) | Fullstack, SSR, API routes |
| Language | TypeScript | Type safety, learning investment |
| Styling | Tailwind CSS + ShadCN UI | Rapid UI development |
| Database | PostgreSQL (Supabase) | Reliable, scalable, free tier |
| ORM | Prisma | Type-safe, easy migration |
| Auth | NextAuth.js | Built for Next.js |
| State | Zustand + TanStack Query | Simple & powerful |
| AI | OpenAI API | Best LLM provider |
| Deploy | Vercel | Zero-config Next.js deploy |

---

## ⚡ Development Rules Reminder

1. **MVP First** — Fitur minimal yang memberikan value
2. **No Overengineering** — Jangan pakai microservices, K8s, dll
3. **Commit Sering** — `feat(scope): description`
4. **Refactor Setelah Stabil** — Jangan refactor saat masih develop
5. **Test Manual Dulu** — Automated test nanti setelah MVP stabil
