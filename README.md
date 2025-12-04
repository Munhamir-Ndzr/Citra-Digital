# Citra-Digital

1.Instalasi ModelScope
Jalankan cell pertama dan kedua:

!pip install modelscope
!pip install modelscope==1.9.5

2. Import Library dan Download Model
Jalankan cell berikutnya:

import cv2
from modelscope.outputs import OutputKeys
from modelscope.pipelines import pipeline
from modelscope.hub.snapshot_download import snapshot_download

Lalu:

model_dir = snapshot_download('damo/cv_ddcolor_image-colorization', revision='v1.0.0')
colorizer = pipeline('image-colorization', model=model_dir)
print('Model DDColor berhasil diload.')

fungsi:
Mendownload model DDColor
Menyiapkan pipeline untuk mewarnai gambar

3. Upload Gambar Hitam Putih
Ada cell untuk upload file:

from google.colab import files
import cv2
from matplotlib import pyplot as plt

uploaded = files.upload()
img_path = list(uploaded.keys())[0]

Setelah menjalankan cell ini:
Klik Choose File
Pilih gambar hitam putih (format JPG/PNG)

4. Proses Colorization
Jalankan cell berikutnya:

img = cv2.imread(img_path)
result = colorizer(img)
colorized_img = result[OutputKeys.OUTPUT_IMG]

6. Tampilkan Hasil
Notebook juga menampilkan hasil dengan Matplotlib:

plt.figure(figsize=(12,6))
plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original")

plt.subplot(1,2,2)
plt.imshow(cv2.cvtColor(colorized_img, cv2.COLOR_BGR2RGB))
plt.title("Colorized")
plt.show()
