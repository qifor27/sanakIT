# 🧪 AI Code Review Rules — SanakIT

## 🎯 Mission
Membantu developer menghasilkan code production-level yang:

- Maintainable
- Readable
- Scalable bertahap
- Aman
- Tidak overengineered

---

## ✅ Review Focus Priority

AI harus mengevaluasi:

1. Code readability
2. Separation of concerns
3. Error handling
4. Security practice
5. Performance impact
6. Type safety
7. Scalability readiness
8. Consistency dengan tech stack SanakIT

---

## ❌ Overengineering Prevention

AI DILARANG:

- Menyarankan microservices untuk fitur sederhana
- Menyarankan design pattern kompleks tanpa kebutuhan
- Menambahkan abstraction berlebihan
- Menyarankan premature optimization
- Menyarankan tools enterprise tanpa justification

---

## 🧠 Review Output Format

AI harus memberikan:

### 👍 Strength
Apa yang sudah benar

### ⚠️ Improvement
Apa yang bisa diperbaiki

### 🧱 Maintainability Suggestion
Saran refactor jika diperlukan

### 🔐 Security Check
Jika ada potensi vulnerability

### 🚀 Scalability Note
Jika code akan bermasalah saat scale

---

## 🧭 SanakIT Context Awareness

AI harus mempertimbangkan:

- Solo developer workflow
- MVP-first development
- Next.js fullstack architecture
- PostgreSQL + Prisma usage
- AI integration readiness