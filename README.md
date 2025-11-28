# Sistem Informasi Raport RQM

Aplikasi web untuk manajemen raport santri di Rumah Qur'an Muharrik (RQM).

## 🚀 Fitur Utama

### 📊 Manajemen Data
- **Data Santri**: CRUD santri dengan informasi lengkap (NIS, nama, halaqah, dll)
- **Data Guru**: Kelola profil guru dan admin
- **Data Halaqah**: Manajemen kelas/halaqah
- **Tahun Ajaran & Semester**: Pengaturan periode akademik
- **Data Surah**: Master data surah untuk tahfidz

### 📝 Input & Cetak Raport
- **Input Nilai**: Form input nilai Akhlak, Kedisiplinan, Kognitif (Tahsin & Tahfidz)
- **Leger Nilai**: Rekap nilai semua santri per semester
- **Cetak Raport**: 
  - Kustomisasi tema warna
  - Pilihan ukuran kertas (A4/F4)
  - Upload logo lembaga
  - Upload tanda tangan kepala & guru
  - Atur data kop raport

### 👥 User Management
- **Role-based Access**: Admin, Guru, Viewer
- **Edit Profil**: Nama lengkap dan tanda tangan
- **Dashboard Khusus**: Tampilan berbeda untuk Admin dan Guru

## 🛠️ Tech Stack

- **Frontend**: React + TypeScript + Vite
- **Styling**: Tailwind CSS
- **UI Components**: Shadcn/ui + Radix UI
- **State Management**: TanStack Query (React Query)
- **Backend**: Supabase (PostgreSQL + Auth + Storage)

## 📋 Prerequisites

- Node.js 18+ dan npm
- Akun Supabase (free tier sudah cukup)

## ⚙️ Setup & Installation

### 1. Clone Repository

```bash
git clone https://github.com/supabasekedua/raport-rqm.git
cd raport-rqm
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Setup Supabase

1. Buat project baru di [Supabase](https://supabase.com)
2. Copy **Project URL** dan **anon key** dari Settings → API
3. Buat file `.env` di root folder:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
```

### 4. Run Database Migrations

Jalankan semua file SQL di folder `supabase_schema/` secara berurutan di Supabase SQL Editor:

```
001_create_tables.sql
002_policies.sql
003_create_triggers.sql
004_seed_surah.sql
005_add_tahfidz_progress.sql
006_add_semester.sql
007_add_user_details.sql
008_fix_users_policies.sql
009_add_halaqah_fk.sql
010_add_footer_raport.sql
011_allow_view_all_users.sql
012_fix_tahfidz_relationship.sql
013_add_headmaster_signature.sql
014_storage_setup.sql
015_fix_signatures_and_rls.sql
```

### 5. Create First Admin User

1. Buka Supabase Dashboard → Authentication → Users
2. Klik **"Add user"** → **"Create new user"**
3. Masukkan email dan password
4. Setelah user dibuat, buka **SQL Editor** dan jalankan:

```sql
UPDATE public.users 
SET role = 'admin', full_name = 'Admin RQM'
WHERE email = 'your-email@example.com';
```

### 6. Run Development Server

```bash
npm run dev
```

Aplikasi akan berjalan di `http://localhost:5173`

## 📖 Cara Penggunaan

### Login Pertama Kali
1. Buka aplikasi di browser
2. Login dengan email dan password admin yang sudah dibuat
3. Anda akan masuk ke Dashboard

### Setup Data Master
1. **Tahun Ajaran**: Buat tahun ajaran baru (misal: 2024/2025)
2. **Semester**: Buat semester (Ganjil/Genap) dan set sebagai aktif
3. **Halaqah**: Buat kelas/halaqah dan assign guru
4. **Santri**: Input data santri dan assign ke halaqah
5. **Pengaturan**: Isi data lembaga, bobot nilai, dan footer raport

### Input Nilai Raport
1. Pilih menu **"Input Raport"**
2. Filter santri berdasarkan halaqah
3. Klik **"Input Nilai"** pada santri yang dipilih
4. Isi nilai Akhlak, Kedisiplinan, Kognitif, dan Tahfidz
5. Klik **"Simpan"**

### Cetak Raport
1. Setelah input nilai, klik **"Cetak Raport"**
2. Atur kustomisasi (tema, logo, tanda tangan) di sidebar
3. Klik **Print** atau **Save as PDF** dari browser

## 🔐 User Roles

| Role | Akses |
|------|-------|
| **Admin** | Full access - semua fitur |
| **Guru** | Input nilai, cetak raport untuk halaqah sendiri |
| **Viewer** | Hanya lihat data (untuk wali santri) |

## 📁 Struktur Folder

```
raport-rqm/
├── src/
│   ├── components/      # Reusable components
│   │   ├── layout/      # Layout components
│   │   ├── raport/      # Raport-specific components
│   │   └── ui/          # UI primitives (shadcn)
│   ├── hooks/           # Custom React hooks
│   ├── lib/             # Utilities & Supabase client
│   ├── pages/           # Page components
│   │   ├── auth/        # Login page
│   │   ├── dashboard/   # Dashboard
│   │   ├── master/      # Master data pages
│   │   ├── raport/      # Raport pages
│   │   ├── settings/    # Settings page
│   │   └── users/       # User management
│   └── types/           # TypeScript types
├── supabase_schema/     # Database migrations
└── public/              # Static assets
```

## 🚀 Deployment

### Deploy ke Vercel (Recommended)

1. Push kode ke GitHub (sudah dilakukan ✅)
2. Buka [Vercel](https://vercel.com)
3. Import repository `supabasekedua/raport-rqm`
4. Tambahkan Environment Variables:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
5. Deploy!

### Deploy ke Netlify

```bash
npm run build
```

Upload folder `dist/` ke Netlify atau connect repository.

## 🐛 Troubleshooting

### "Data not found" saat cetak raport
- Pastikan sudah ada semester aktif
- Pastikan nilai sudah disimpan

### Upload tanda tangan gagal
- Jalankan migration `014_storage_setup.sql` dan `015_fix_signatures_and_rls.sql`
- Pastikan storage bucket `raport-assets` sudah dibuat

### User tidak bisa login
- Cek apakah user sudah dikonfirmasi di Supabase Auth
- Pastikan RLS policies sudah dijalankan

## 📝 License

MIT License - bebas digunakan dan dimodifikasi

## 👨‍💻 Developer

Developed for Rumah Qur'an Muharrik (RQM)

---

**Need Help?** Open an issue di GitHub repository ini.
