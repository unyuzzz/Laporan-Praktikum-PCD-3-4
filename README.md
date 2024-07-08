# Laporan-Praktikum-PCD-3-4

## garis dan tepi
- Python
- numpy
- scikit-image
- matplotlib

yang dimana pada pengerjaannya terdapat beberapa pustaka yang diperlukan dan kemudian perlu membaca file gambar yang akan dieksekusi,
terkait pengaturan untuk eksekusi itu terdapat pengubahan untuk bisa diubah jadi grayscale terlebih dahulu yang kemudian
nantinya akan dideteksikan terkait tepi yang ada pada gambar
``` bash
#mengatur perubahan untuk menjadi grayscale serta mendeteksi tepi nanti.
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(image,100,150)

#ini sama seperti cell sebelumnya, dan ini akan nampilin lewat window nantinya
cv2.imshow("parkiran mobil", edges)
cv2.waitKey(0)
cv2.destroyAllWindows()

#bagian untuk nampilin hasil dari grayscale dengan tepi
fig, axs = plt.subplots(1,2,figsize = (10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap = "gray")
ax[0].set_title("Gambar Asli")

ax[1].imshow(edges, cmap = "gray")
ax[1].set_title("Gambar yang udah")

```
kemudian terkait deteksi untuk garis hough
```
#deteksi garis dengan transformasi hough
lines = cv2.HoughLinesP(edges,1,np.pi/180,30,maxLineGap=250) #function
image_line = image.copy()

for line in lines:
    x1,y1,x2,y2 = line [0]
    cv2.line(image_line,(x1,y1),(x2,y2),(100,8,255),1)
kemudian ditampilkan pada bagian :
fig,axs = plt.subplots(1,2,figsize = (10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap = "gray")
ax[0].set_title("Gambar Asli")

ax[1].imshow(image_line, cmap = "gray")
ax[1].set_title("Gambar yang udah")
```
## ekstraksi fitur
- python
- numpy
- skimage
- matplotlib

dari gambar yang akan dieksekusi itu sama, namun pada bagian pengaturan untuk eksekusi untuk diekstrakti kan gambar nya
dia menggunakan saluran hue untuk hist dan juga bins nya, nah pada bagian ini diatur mengenai histogram dari numpy dengan
```bash
(hsv_image[:, :, 0], bins=256, range=(0, 1))

kemudian adanya bagian untuk menampilkan hasil gambar ekstraksinya
#bagian untuk menampilkan hasil ekstraksinya
fig, axes = plt.subplots(1, 2, figsize=(12, 6))
axes[0].imshow(image)
axes[0].set_title('Gambar Asli')
axes[0].axis('off')

axes[1].imshow(hsv_image)
axes[1].set_title('Gambar HSV')
axes[1].axis('off')

plt.show()
#gak pake plt.show() pun gapapa

kemudian terdapat hasil dari hsv histogramnya itu disimpan terkait saluran hue nya
np.savetxt('hsv_histogram.txt', hue_hist)
print("Histogram saluran Hue disimpan sebagai 'hsv_histogram.txt'")
#note : ini lebih ke menyimpan histogramnya sebagai file teks
