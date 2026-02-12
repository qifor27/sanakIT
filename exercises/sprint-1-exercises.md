# 🏋️ Sprint 1 Exercises — Project Setup & Foundation

> Kerjakan latihan ini setelah mempelajari materi Sprint 1.
> Tujuannya memastikan kamu benar-benar paham, bukan copy-paste.

---

## Exercise 1: TypeScript Basics ⭐

### Soal
Tulis TypeScript type untuk data **User** SanakIT dengan ketentuan:
- `id` → string (wajib)
- `email` → string (wajib)
- `name` → string (wajib)
- `bio` → string (opsional)
- `role` → hanya boleh "MEMBER", "MENTOR", atau "ADMIN"
- `createdAt` → Date

### Hint
```typescript
// Gunakan type alias atau interface
// Gunakan union type untuk role
// Gunakan optional property (?) untuk bio
```

### Jawaban (buka setelah coba sendiri)
<details>
<summary>Klik untuk melihat jawaban</summary>

```typescript
// Cara 1: Menggunakan Type Alias
type Role = "MEMBER" | "MENTOR" | "ADMIN"

type User = {
  id: string
  email: string
  name: string
  bio?: string      // ? artinya optional
  role: Role
  createdAt: Date
}

// Cara 2: Menggunakan Interface
interface IUser {
  id: string
  email: string
  name: string
  bio?: string
  role: "MEMBER" | "MENTOR" | "ADMIN"
  createdAt: Date
}
```

**Penjelasan:**
- `?` setelah property name artinya property itu opsional
- Union type (`"MEMBER" | "MENTOR" | "ADMIN"`) membatasi value yang valid
- `type` vs `interface`: keduanya mirip, `interface` bisa di-extend, `type` lebih fleksibel

</details>

---

## Exercise 2: React Component ⭐

### Soal
Buat component `UserCard` yang menerima props user (dari Exercise 1) dan menampilkan:
- Nama user
- Email
- Role (dengan badge warna berbeda)
- Bio (jika ada)

### Hint
```tsx
// Gunakan type dari Exercise 1 sebagai props type
// Gunakan conditional rendering untuk bio
// Gunakan Tailwind untuk styling
```

### Jawaban
<details>
<summary>Klik untuk melihat jawaban</summary>

```tsx
// components/shared/UserCard.tsx

type Role = "MEMBER" | "MENTOR" | "ADMIN"

type User = {
  id: string
  email: string
  name: string
  bio?: string
  role: Role
  createdAt: Date
}

// Object untuk mapping warna badge per role
const roleBadgeColors: Record<Role, string> = {
  MEMBER: "bg-blue-100 text-blue-800",
  MENTOR: "bg-green-100 text-green-800",
  ADMIN: "bg-red-100 text-red-800",
}

export function UserCard({ user }: { user: User }) {
  return (
    <div className="rounded-lg border p-4 shadow-sm">
      {/* Nama */}
      <h3 className="text-lg font-semibold">{user.name}</h3>

      {/* Email */}
      <p className="text-sm text-gray-500">{user.email}</p>

      {/* Role Badge */}
      <span className={`mt-2 inline-block rounded-full px-2 py-1 text-xs font-medium ${roleBadgeColors[user.role]}`}>
        {user.role}
      </span>

      {/* Bio - conditional rendering */}
      {user.bio && (
        <p className="mt-2 text-sm text-gray-600">{user.bio}</p>
      )}
    </div>
  )
}
```

**Penjelasan:**
- `Record<Role, string>` → TypeScript utility type untuk object dengan key type tertentu
- `{user.bio && (...)}` → conditional rendering, hanya render jika `bio` ada
- Props destructured langsung: `{ user }: { user: User }`
- Tailwind classes untuk styling tanpa CSS file terpisah

</details>

---

## Exercise 3: Next.js Routing ⭐⭐

### Soal
Jelaskan (tulis di learning-notes.md) perbedaan antara:
1. `app/page.tsx` — halaman apa?
2. `app/community/page.tsx` — halaman apa?
3. `app/community/[id]/page.tsx` — halaman apa? Apa itu `[id]`?
4. `app/(auth)/login/page.tsx` — kenapa ada `(auth)` dengan kurung?
5. `app/api/posts/route.ts` — ini apa bedanya dengan `page.tsx`?

### Jawaban
<details>
<summary>Klik untuk melihat jawaban</summary>

1. **`app/page.tsx`** → Halaman root / homepage (`localhost:3000/`)
2. **`app/community/page.tsx`** → Halaman community (`localhost:3000/community`)
3. **`app/community/[id]/page.tsx`** → Dynamic route. `[id]` adalah parameter.
   - `/community/abc123` → `id = "abc123"`
   - Bisa diakses via `params.id` di component
4. **`app/(auth)/login/page.tsx`** → Route Group. `(auth)` tidak muncul di URL.
   - URL tetap `/login`, bukan `/auth/login`
   - Berguna untuk grouping layout (misal auth pages punya layout berbeda)
5. **`app/api/posts/route.ts`** → API Route / Route Handler.
   - Bukan halaman, tapi endpoint API
   - Handle `GET`, `POST`, `PUT`, `DELETE` requests
   - Contoh: `GET /api/posts` return data posts

</details>

---

## Exercise 4: Prisma Schema ⭐⭐

### Soal
Tulis Prisma schema untuk tabel `learning_paths` dengan ketentuan:
- `id` → cuid, primary key
- `title` → string, wajib
- `description` → string, wajib
- `difficulty` → enum (BEGINNER, INTERMEDIATE, ADVANCED)
- `authorId` → foreign key ke tabel `users`
- `createdAt` dan `updatedAt` → timestamp otomatis
- Nama tabel di database: `learning_paths`

### Hint
```prisma
// Gunakan @id @default(cuid())
// Gunakan @map untuk column name
// Gunakan @@map untuk table name
// Gunakan @relation untuk foreign key
```

### Jawaban
<details>
<summary>Klik untuk melihat jawaban</summary>

```prisma
enum Difficulty {
  BEGINNER
  INTERMEDIATE
  ADVANCED
}

model LearningPath {
  id          String     @id @default(cuid())
  title       String
  description String
  difficulty  Difficulty @default(BEGINNER)
  authorId    String     @map("author_id")
  author      User       @relation(fields: [authorId], references: [id])
  createdAt   DateTime   @default(now()) @map("created_at")
  updatedAt   DateTime   @updatedAt @map("updated_at")

  @@map("learning_paths")
}
```

**Penjelasan:**
- `@id @default(cuid())` → Primary key dengan auto-generate CUID
- `@map("author_id")` → Column di DB bernama `author_id`, tapi di code tetap `authorId` (camelCase)
- `@@map("learning_paths")` → Nama tabel di database
- `@relation(fields: [authorId], references: [id])` → Foreign key relationship
- `@default(now())` → Auto-fill timestamp saat record dibuat
- `@updatedAt` → Auto-update timestamp saat record di-update

</details>

---

## Exercise 5: Folder Structure ⭐

### Soal
Buat folder structure (kosong) sesuai arsitektur SanakIT yang sudah ditentukan.
Jalankan perintah ini di terminal:

```bash
# Latihan: Buat folder structure sendiri
# Setelah selesai, bandingkan dengan arsitektur di MVP Sprint Plan
```

Coba buat manual folder-folder berikut dan jelaskan fungsi masing-masing:
- `src/app/`
- `src/components/ui/`
- `src/features/`
- `src/lib/`
- `src/hooks/`
- `src/services/`
- `src/types/`

### Jawaban
<details>
<summary>Klik untuk melihat jawaban</summary>

| Folder | Fungsi |
|--------|--------|
| `src/app/` | Next.js App Router — routing & pages |
| `src/components/ui/` | ShadCN reusable UI components (Button, Input, dll) |
| `src/features/` | Feature modules (auth, community, mentor) — **separation of concerns** |
| `src/lib/` | Utility & config (prisma client, auth config, helpers) |
| `src/hooks/` | Custom React hooks (reusable logic) |
| `src/services/` | API service layer (fetch functions) |
| `src/types/` | TypeScript type definitions |

**Kenapa pakai Feature-Based Structure?**
- Lebih mudah dicari (semua terkait auth ada di `features/auth/`)
- Lebih mudah di-maintain saat project membesar
- Best practice untuk production-level apps

</details>

---

## 🏆 Scoring

| Score | Level |
|-------|-------|
| 5/5 benar | 🌟 Siap Sprint 1! |
| 3-4 benar | 👍 Review sekali lagi |
| 1-2 benar | 📚 Pelajari ulang materi |

> **Tips:** Jangan langsung lihat jawaban. Coba tulis sendiri dulu, lalu bandingkan!
