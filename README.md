# 📚 Bimbel Ahe — Aplikasi Manajemen Operasional

A complete, **zero-dependency** operational management web app for a tutoring center,
built from the AppSheet blueprint as a real running application.

Open `index.html` in any browser. That's it — no install, no server, no internet required.
Data is saved in the browser (`localStorage`) and survives refreshes.

---

## ✅ What's implemented (mapped to your blueprint)

| Blueprint item | In this app |
|---|---|
| **3 tables** (Data Murid, Data Guru, Log Sesi) | 3 data stores with Ref-style links between them |
| **Google SSO + email whitelist** | Teacher login screen checking `CONFIG.whitelist` (swap for real SSO later) |
| **Hidden system IDs** | IDs are auto-generated and never shown in the UI |
| **New-student form shows only static fields** | Nama + No HP + Kuota; dynamic fields (SPP, Level, Sisa Kuota) hidden on registration |
| **2-page Log Sesi form** | Stepper: Page 1 (Guru, Waktu Selesai, Durasi) → Page 2 (Level, Page Awal/Akhir, Total, Catatan, Foto) |
| **Queue dashboard grouped by status** | Waiting → In Progress → Done, each group sorted oldest-first |
| **"Claim Murid" prominent action** | Large primary button on the detail sheet; sets status → In Progress |
| **`Sisa Kuota Sesi` App Formula** | `Kuota Awal − COUNT(logs for this murid)`, computed live |
| **`Total Page` / `Durasi Belajar` auto-calc** | Computed automatically in the form, shown in dashed "otomatis" boxes |
| **Custom color + logo branding** | Set in `:root { --brand }` and `CONFIG.logo` |

**Max-3-clicks flow:** Antrian → tap student → **Klaim Murid** → form opens automatically.

---

## 🔑 Demo login
Use `admin@bimbelahe.com` (also `guru1@` / `guru2@bimbelahe.com`).

---

## 🎨 Rebrand in 10 seconds
- **Color:** edit `--brand` in the `:root` CSS block.
- **Logo / name:** edit `CONFIG.logo`, `CONFIG.appName`, `CONFIG.tagline`.
- **Teacher access list:** edit `CONFIG.whitelist`.
- **Levels / SPP options:** edit `CONFIG.levels`, `CONFIG.sppStatus`.

---

## 🚀 Deploy options
- **GitHub Pages / Netlify Drop / Vercel:** just upload `index.html`.
- **Google Sites:** embed as an HTML file.
- Works offline as a mobile "Add to Home Screen" web app.

---

## 🔁 Upgrading to real Google Sheets + SSO later
The data layer is isolated in the `DB` object and the login in `Session` + `LoginView`.
To make it a true cloud app, replace:
1. `DB.read/write` → calls to the Google Sheets API (or any backend).
2. `LoginView` → Google Identity Services (OAuth), keeping the same whitelist check.

Everything else (formulas, forms, queue, actions) stays the same.
