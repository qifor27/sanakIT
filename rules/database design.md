DATABASE DESIGN RULE
🎯 Tujuan

Membuat database yang:

Mudah dikembangkan

Tidak redundant

Mudah dipahami mahasiswa

Siap untuk scale startup

✅ Prinsip Utama
1. Gunakan Normalisasi Dasar

Minimal sampai 3rd Normal Form

1 Table = 1 Entity
2. Gunakan Naming Convention Konsisten
Table
snake_case

Contoh:

users
learning_paths
user_projects
mentor_sessions
Column
snake_case

Contoh:

created_at
updated_at
user_id
learning_path_id
3. Gunakan Primary Key Standar

Gunakan:

id (UUID / CUID)
4. Wajib Timestamp

Semua table wajib memiliki:

created_at
updated_at
5. Gunakan Foreign Key Dengan Jelas

Contoh:

user_id → users.id
6. Hindari Over Relationship

Jika belum diperlukan:

❌ Many to many kompleks
❌ Polymorphic relation terlalu awal

7. Gunakan Enum Untuk Status

Contoh:

status:
- draft
- published
- archived
📦 Struktur Database Default SanakIT
users
profiles
learning_paths
courses
lessons
projects
community_posts
mentor_sessions
career_progress