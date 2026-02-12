♻️ REFACTORING RULE
🎯 Tujuan

Meningkatkan kualitas code tanpa mengubah behavior.

✅ Kapan Refactor?

Function terlalu panjang (>40 line)

Logic sulit dipahami

Duplicate code

Naming tidak jelas

✅ Prinsip Refactor
1. Small Step Refactor
Refactor sedikit tapi sering
2. Gunakan Single Responsibility
1 function = 1 purpose
3. Extract Reusable Logic

Pindahkan ke:

utils
services
hooks
4. Refactor Setelah Feature Stabil
❌ Jangan Refactor Jika

Deadline dekat

Tidak ada test

Tidak paham logic