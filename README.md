# UAS_PengolahanCitra_4
---
# Anggota Kelompok
| Name  | NIM |
| ----- | --- |
| Vivie Zuliani Erikasari   | 312210475  |
| Zulaeha | 312210575  |
| Tyanshi Firli Maharani   | 312210581  |
| Wafha Zahra Mulqiya | 312210577  |
| Alfaza Putra Adjie Ariefiansyah   | 312210512  |

---

# Daftar Isi
1. Kode program RGB KMeans
2. Hasil output dari image yang di input
3. Kode KMeans Clustering
4. Hasil output foto yang telah di lakukan Clustering
5. Dimensi foto berdasarkan tipe HP

---

### PROGRAM RGB KMEANS UNTUK FOTO TAS
###### Terdapat 5 jenis kamera untuk dilakukan perubahan terhadap 1 jenis tas yang di uji K-Meansnya. Tas yang diuji meliputi sisi depan dan sisi samping


* Pertama-tama memanggil fungsi numpy, matplotlib dan cv2 agar nantinya file bisa terdeteksi
```
import numpy as np
import matplotlib.pyplot as plt
import cv2
```

* Kode untuk memanggil gambar yang akan dilakukan perubahan
```
# untuk membaca gambar gunakan gambar sesuai dengan yg dimiliki
image = cv2.imread("C:\\Users\\Vivie Zuliani\\Pictures\\images\\sisidepan.jpg")
image = cv2.imread("C:\\Users\\Vivie Zuliani\\Pictures\\images\\sisisamping.jpg")
```

* Kode untuk mengubah gambar ke RGB dari BGR
```
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
plt.imshow(image)
```

## Hasil Penginputan Foto Tas

Berikut merupakan hasil foto setelah foto di input melalui ``image = cv.imread("")`` : 

> Sisi Depan

![Screenshot 2024-07-09 125313](https://github.com/VivieZuliani/UAS_PengolahanCitra_4/assets/130271255/1a6f8b48-7f25-49c9-91c9-ef8d5246bc76)

> Sisi Samping

![Screenshot 2024-07-09 152926](https://github.com/VivieZuliani/UAS_PengolahanCitra_4/assets/130271255/48a98c16-9bbd-4920-970b-08e0c9573f66)

---

* Kemudian lakukan pembentukan susunan ulang dan konversikan ke tipe float serta ubah akurasi menjadi 85%
```
pixel_vals = image.reshape((-1,3))
pixel_vals = np.float32(pixel_vals)
criteria = (cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER, 100, 0.85)
```

* Lakukan KMeans clustering, untuk K=3 dan konversikan menjadi 8 bit
```
k = 3
retval, labels, centers = cv2.kmeans(pixel_vals, k, None, criteria, 10, cv2.KMEANS_RANDOM_CENTERS)

centers = np.uint8(centers)
segmented_data = centers[labels.flatten()]

# membentuk ulang data menjadi dimensi gambar asli
segmented_image = segmented_data.reshape((image.shape))
plt.imshow(segmented_image)
```

## Hasil setelah dilakukan K-Means : 

> Sisi Depan

![Screenshot 2024-07-09 150649](https://github.com/VivieZuliani/UAS_PengolahanCitra_4/assets/130271255/1f8c394c-b72a-4ee1-bd87-79c4d4b4ffc3)

> Sisi Samping

![Screenshot 2024-07-09 153054](https://github.com/VivieZuliani/UAS_PengolahanCitra_4/assets/130271255/e47a2eb1-7fff-4664-8cae-b0f7b5f4755e)

---

##  DIMENSI FOTO TAS BERDASARKAN TIPE HANDPHONE  
| Jenis Handphone  | Sisi Depan(Pixel) | Sisi Samping(Pixel) | Bit |
| ----- | --- | --- | --- |
| Redmi Note 10  | 3000 x 4000  | 3000 x 4000 | 24 |
| Realme C53 | 900 x 1600  | 900 x 1600 | 24 | 
| Infinix Hot 11 Play | 3120 x 4160  | 3120 x 4160 | 24 | 
| Samsung A04E | 3120 x 4160  | 3120 x 4160 | 24 | 
| Infinix Zero 30 | 2976 x 3968  | 2976 x 3968 | 24 | 

> Terdapat perbedaan pixel pada masing-masing handphone. Namun, antara handphone Infinix Hot 11 Play dan Samsung A04E memiliki persamaan pada pixel nya. Untuk ukuran bit semua tipe handphone di atas memiliki kesamaan yaitu `24 bit`

## SELESAI
# Terima kasih











