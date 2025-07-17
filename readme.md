# 📘 REST API - Manajemen Pengguna (CodeIgniter 3 + JWT)

REST API ini dibuat menggunakan CodeIgniter 3 untuk manajemen pengguna, dilengkapi autentikasi menggunakan JWT.

---

## 📁 Struktur Utama

- `application/controllers/Auth.php` → login dan generate token JWT
- `application/controllers/User.php` → endpoint CRUD user (dilindungi token)
- `application/models/User_model.php` → query ke database users

---

## 🚀 Cara Menjalankan di XAMPP

### 1. Clone / Extract Project ke `htdocs`

```
C:/xampp/htdocs/ci3-jwt-api/
```

### 2. Buat Database

- Import file SQL 'user_api.sql'

### 3. Konfigurasi Database

Edit file: `application/config/database.php`

```php
$db['default'] = array(
  'hostname' => 'localhost',
  'username' => 'root',
  'password' => '',
  'database' => 'user_api',
  'dbdriver' => 'mysqli',
  ...
);
```

### 4. Konfigurasi base_url

Edit file: `application/config/config.php`

```php
$config['base_url'] = 'http://localhost/tesRumahweb/Codeigniter/';
```

### 5. Install Composer (untuk JWT)

install Composer JWT:

```bash
cd tesRumahweb
composer require firebase/php-jwt
```

> Jika tidak ingin pakai Composer, bisa salin file JWT manual ke folder library dan load secara manual (tidak disarankan).

---

## 🔐 Autentikasi

Gunakan endpoint berikut untuk login dan mendapatkan token:

### 🔸 Login

**POST** `/auth/login`

#### Request Body (JSON):

```json
{
  "email": "alaufa@example.com",
  "password": "123456"
}
```

#### Response:

```json
{
  "token": "<jwt_token>"
}
```

Simpan token ini untuk digunakan pada semua endpoint berikutnya.

---

## 📦 Endpoint CRUD Users (dilindungi JWT)

Semua endpoint di bawah harus menambahkan Header:

```
Authorization: Bearer <token-dari-login>
```

### 1. Get Products

```
GET /user
```

### 2. ADD Products

```
POST /user/store
```

**Body:**

```json
{
  "name": "komputer",
  "price": "10000000",
  "category_id": "1"
}
```

### 4. Update Product

```
PUT /user/update/{id}
```

**Body:**

```json
{
  "name": "Produk baru",
  "price": "10000000",
  "category_id": "1"
}
```

### 5. Delete User

```
DELETE /user/delete/{id}
```

---

## 📬 Testing dengan Postman

Gunakan `postman collection.json` yang disediakan untuk import langsung semua endpoint.

Jangan lupa isi:

- `Authorization` header: `Bearer <token>`
- Pilih metode sesuai (GET, POST, PUT, DELETE)

---
