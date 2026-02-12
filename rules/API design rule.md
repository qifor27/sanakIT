API DESIGN RULE
🎯 Tujuan

Membuat API yang:

Konsisten

Mudah dibaca

RESTful

Mudah di-maintain

✅ REST Naming Convention
Gunakan Noun, Bukan Verb
GET    /courses
POST   /courses
GET    /courses/:id
PUT    /courses/:id
DELETE /courses/:id
✅ Struktur Response Standar
{
  "success": true,
  "message": "Data fetched successfully",
  "data": {}
}
✅ Struktur Error Response
{
  "success": false,
  "message": "Course not found"
}
✅ Versioning API
/api/v1/
✅ Validasi Input

Gunakan:

Zod

Joi

Yup

❌ Dilarang

Response tidak konsisten

Business logic terlalu berat di controller

Hardcoded data