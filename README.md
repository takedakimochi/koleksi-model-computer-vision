# 🤖 Koleksi Model Computer Vision (YOLOv8 Repository)

Selamat datang di **Gudang Harta Karun Computer Vision**! 🚀  
Folder ini isinya kumpulan *pre-trained weight* (`.pt`) model **YOLOv8** yang udah siap pakai buat berbagai kebutuhan *object detection*, mulai dari yang standar sampai yang spesifik kayak deteksi wajah, helm, kepala, manusia, drone, tempat parkir, hingga plat nomor kendaraan Indonesia!

---

## 📁 Struktur Folder & Daftar Model

Berikut adalah peta lokasi harta karun model yang ada di dalam repository ini:

```text
koleksi-model-computer-vision/
├── README.md
└── Yolo/
    ├── helm/                       # 🪖 Model Deteksi Kepala & Helm (NLF)
    │   ├── yolov8n-nlf-head-detection.pt
    │   ├── yolov8s-nlf-head-detection.pt
    │   └── yolov8m-nlf-head-detection.pt
    │
    ├── kepala/                     # 🗣️ Model Deteksi Kepala
    │   └── kepala.pt
    │
    ├── lain-lain/                  # 🛸 Model Spesifik Lainnya
    │   ├── yolov8m-drone.pt        # Deteksi Drone di Udara (Medium)
    │   ├── yolov8m-football.pt     # Deteksi Bola & Pemain Sepak Bola (Medium)
    │   └── yolov8m-parking.pt      # Deteksi Mobil & Slot Parkir (Medium)
    │
    ├── manusia/                    # 🧍 Model Deteksi Manusia
    │   └── yolov8n_person.pt       # Deteksi Orang/Manusia (Nano)
    │
    ├── plat_nomor/                 # 🚘 Model Deteksi Plat Nomor Indonesia
    │   ├── yolov8s_box_plat_nomor_indonesia_1280.pt   # Bounding Box Plat Nomor (Res 1280)
    │   └── yolov8s_huruf_angka_plat_nomor_indonesia_640.pt # Deteksi Karakter Huruf & Angka (Res 640)
    │
    └── wajah/                      # 👤 Model Deteksi Wajah (Face Detection)
        ├── yolov8n-face.pt         # Face Detection Nano
        ├── yolov8m-face.pt         # Face Detection Medium
        └── yolov8l-face.pt         # Face Detection Large (Akurasi paling mantap)
```

---

## 🎯 Detail & Use-Case Model

### 1. 👤 Deteksi Wajah (`Yolo/wajah/`)
Model khusus buat nemuin posisi wajah di gambar/video stream:
* **`yolov8n-face.pt`**: Sangat cocok buat device hemat daya/Edge Devices (Raspberry Pi, HP, webcam laptop kentang).
* **`yolov8m-face.pt`**: Pilihan seimbang buat server / PC dengan GPU standar.
* **`yolov8l-face.pt`**: Paling akurat, cocok buat deteksi wajah jarak jauh atau gambar beresolusi tinggi.

### 2. 🪖 Deteksi Kepala & Helm (`Yolo/helm/`)
Model spesifik buat cek orang pake helm atau enggak (cocok buat sistem K3 / Keselamatan Kerja atau TILANG Elektronik):
* **`yolov8n-nlf-head-detection.pt`**
* **`yolov8s-nlf-head-detection.pt`**
* **`yolov8m-nlf-head-detection.pt`**

### 3. 🗣️ Deteksi Kepala (`Yolo/kepala/`)
Model khusus untuk mendeteksi bagian kepala:
* **`kepala.pt`**: Model deteksi kepala versi medium (50MB) yang presisi buat ngenali kepala manusia.

### 4. 🧍 Deteksi Manusia (`Yolo/manusia/`)
Model khusus fokus ke objek manusia:
* **`yolov8n_person.pt`**: Versi Nano super enteng khusus deteksi manusia/person.

### 5. 🚘 Deteksi Plat Nomor Indonesia (`Yolo/plat_nomor/`)
Model *custom-tuned* buat membaca kendaraan dan plat nomor di Indonesia:
* **`yolov8s_box_plat_nomor_indonesia_1280.pt`**: Mencari area/kotak plat nomor pada kendaraan (Image size: 1280px).
* **`yolov8s_huruf_angka_plat_nomor_indonesia_640.pt`**: Membaca karakter angka dan huruf pada plat nomor (Image size: 640px).

### 6. 🛸 Model Spesifik Lainnya (`Yolo/lain-lain/`)
* **`yolov8m-drone.pt`**: Memantau dan mendeteksi objek drone di langit.
* **`yolov8m-football.pt`**: Mengacak-acak dan mendeteksi bola serta pemain di lapangan hijau.
* **`yolov8m-parking.pt`**: Analisis tempat parkir dan ketersediaan slot kendaraan.

---

## 🚀 Cara Penggunaan (Quick Start)

Pastikan lu udah install library `ultralytics` dan `opencv-python`:

```bash
pip install ultralytics opencv-python
```

### Contoh Kode Python untuk Inferensi

```python
import cv2
from ultralytics import YOLO

# 1. Pilih model yang mau dipakai (contoh: Deteksi Wajah)
model_path = "Yolo/wajah/yolov8m-face.pt"
model = YOLO(model_path)

# 2. Jalankan deteksi pada gambar atau video
source = "sample.jpg"  # bisa diganti dengan path gambar, video, atau 0 (webcam)
results = model(source, conf=0.5)

# 3. Tampilkan hasil
for r in results:
    im_array = r.plot()  # Gambar bounding box hasil deteksi
    cv2.imshow("Hasil Deteksi", im_array)
    cv2.waitKey(0)

cv2.destroyAllWindows()
```

---

## 💡 Tips Memilih Ukuran Model (Variant)

* **Nano (`n`)**: Super cepat, VRAM irit, cocok buat real-time di hardware terbatas. Akurasi standar.
* **Small (`s`)**: *Sweet spot* antara kecepatan dan akurasi untuk pengujian harian.
* **Medium (`m`)**: Akurasi tinggi, butuh GPU menengah.
* **Large (`l`)**: Akurasi maksimal, butuh spesifikasi GPU mantap.

---
*Happy Coding & Detection!* 💥

