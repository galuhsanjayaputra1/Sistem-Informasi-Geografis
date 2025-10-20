<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/a0bef34b-24fb-429c-9077-96a146d03e60" /># GeoJSON Jalan Kelurahan Melong

Repository ini berisi data 6 jalan di Kelurahan Melong dalam format GeoJSON.  
Setiap jalan disimpan sebagai satu fitur (Feature) dengan tipe geometry `LineString`.

## 📋 Daftar Jalan
1. Jalan Hercules Raya  
2. Jalan Capung  
3. Jalan Foker Raya  
4. Jalan Dahkota Raya  
5. Jalan Foker Tengah 1  
6. Jalan Foker Tengah 2  

Total nilai: 6 jalan × 5 poin = **30 poin**

---

## 🗺️ Cara Mengecek Validitas GeoJSON
1. Buka [https://geojson.io](https://geojson.io)
2. Copy seluruh isi file `roads.geojson` dan paste ke panel kiri
3. Pastikan semua garis jalan muncul di peta
4. Jika tidak error dan semua terlihat, berarti **GeoJSON valid**

---

## 💾 Penyimpanan di MongoDB

Setiap jalan disimpan sebagai **1 dokumen (record)** di MongoDB dengan skema berikut:

| Field        | Type      | Keterangan                           |
|---------------|-----------|--------------------------------------|
| id            | String    | ID unik jalan                        |
| name          | String    | Nama jalan                           |
| village       | String    | Nama kelurahan                       |
| score         | Number    | Maksimal 10                          |
| notes         | String    | Keterangan tambahan                   |
| created_at    | Date      | Tanggal pembuatan data               |
| geometry      | GeoJSON   | Koordinat LineString jalan           |

---

## 🧱 Contoh Model MongoDB (Mongoose)

```js
const mongoose = require('mongoose');

const RoadSchema = new mongoose.Schema({
  id: { type: String, required: true, unique: true },
  name: { type: String, required: true },
  village: { type: String, required: true },
  score: { type: Number, min: 0, max: 10 },
  notes: String,
  created_at: { type: Date, default: Date.now },
  geometry: {
    type: { type: String, enum: ['LineString'], required: true },
    coordinates: [[Number]]
  }
});

module.exports = mongoose.model('Road', RoadSchema);

#
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/82fe0ce5-d955-49da-8d01-d33955c64951" />
