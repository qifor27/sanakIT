# 🧭 SanakIT Development Flow Guide

> Panduan lengkap bagaimana development flow di SanakIT berjalan.

---

## 🔄 Development Flow

```
Idea → Feature Planning → Complexity Check → Sprint Planning → Development → Code Review → Refactor → Deploy
```

---

## 📋 Step-by-Step Guide

### 1. 💡 Idea
Tulis ide fitur yang ingin dibangun.

**Template:**
```
Fitur: [Nama fitur]
Masalah: [Problem yang diselesaikan]
User: [Siapa yang butuh]
Value: [Kenapa penting]
```

---

### 2. 📝 Feature Planning
Gunakan template di `prompts/Feature Planning Prompt Template.md`

Pastikan punya:
- User Story
- Functional Requirements
- Non-functional Requirements

---

### 3. 🔍 Complexity Check

Evaluasi complexity fitur:

| Level | Estimasi | Contoh |
|-------|----------|--------|
| ⭐ Low | < 1 hari | UI component |
| ⭐⭐ Medium | 1-3 hari | CRUD feature |
| ⭐⭐⭐ High | 3-7 hari | AI integration |
| ⭐⭐⭐⭐ Very High | > 1 minggu | Real-time system |

**Rule:** Jika complexity > Medium, **pecah jadi task lebih kecil**.

---

### 4. 🏃 Sprint Planning
Gunakan template di `prompts/sprint planning template.md`

---

### 5. 💻 Development

**Workflow per task:**
```
1. Buat branch: git checkout -b feat/nama-fitur
2. Code fitur
3. Test manual
4. Commit: feat(scope): description
5. Push & review
```

**Coding Rules:**
- Tulis TypeScript
- Ikuti code style convention
- Gunakan Zod untuk validasi
- Error handling yang proper
- Komentar edukatif

---

### 6. 🧪 Code Review
Gunakan checklist dari `rules/AI code review rules.md`:

- [ ] Code readable?
- [ ] Separation of concerns?
- [ ] Error handling proper?
- [ ] Type safety?
- [ ] Security?
- [ ] Performance OK?
- [ ] Tidak overengineered?

---

### 7. ♻️ Refactor
Ikuti aturan di `rules/refactoring rule.md`:

**Refactor HANYA jika:**
- Function > 40 line
- Logic sulit dipahami
- Ada duplicate code
- Naming tidak jelas
- Feature sudah stabil

---

### 8. 🚀 Deploy
- Push ke `main` branch
- Vercel auto-deploy
- Verify di production

---

## 📌 Git Commit Convention

```bash
# Format
type(scope): description

# Contoh
feat(auth): add Google login
fix(community): resolve post loading bug
refactor(api): simplify mentor session logic
docs(readme): update installation guide
style(ui): fix button alignment
test(auth): add login unit test
chore(deps): update dependencies
```

---

## 🔑 Golden Rules

1. **Satu task, satu commit** — Jangan campur banyak perubahan
2. **Test sebelum commit** — Pastikan tidak ada yang rusak
3. **Kecil tapi sering** — Commit kecil lebih aman daripada commit besar
4. **Branch per fitur** — Jangan develop di `main` langsung
5. **Tulis catatan belajar** — Dokumentasikan apa yang kamu pelajari
