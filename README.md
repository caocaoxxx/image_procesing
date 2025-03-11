# 图像基本处理作业

## 环境要求
- Python 3.12
- scikit-image
- matplotlib
- Pillow
- Jupyter lab

## 文件说明
- `assignment1_answer.ipynb`: 包含图像处理的代码示例
- `earth.jpg`, `galaxy-full.jpg`, `x.jpg`: 示例图像文件
- `README.md`: 项目说明文件

## 代码示例说明
`assignment1_answer.ipynb` 文件中包含多个代码单元，每个单元展示了不同的图像处理技术。

### 图像上半部分处理
读取图像并将上半部分的红色通道设置为255：
```python
from skimage import io
import matplotlib.pyplot as plt

img = io.imread('x.jpg')
print(img.shape)
h, w, c = img.shape
for i in range(w):
    for j in range(h//2):
        img[j, i][0] = 255
plt.imshow(img)
plt.show()
```

### 图像左半部分处理
读取图像并将左半部分的红色通道设置为255：
```python
from skimage import io
import matplotlib.pyplot as plt

img = io.imread('x.jpg')
print(img.shape)
h, w, c = img.shape
for i in range(w//2):
    for j in range(h):
        img[j, i][0] = 255
plt.imshow(img)
plt.show()
```

### 图像左上四分之一处理
读取图像并将左上部分的红色通道设置为255：
```python
from skimage import io
import matplotlib.pyplot as plt

img = io.imread('x.jpg')
print(img.shape)
h, w, c = img.shape
for i in range(w//2):
    for j in range(h//2):
        img[j, i][0] = 255
plt.imshow(img)
plt.show()
```

### 小区域像素处理
读取图像并将指定区域的红色通道设置为255：
```python
from skimage import io
import matplotlib.pyplot as plt

img = io.imread('x.jpg')
start_x = 2
start_y = 2
patch_width = 6
patch_height = 6
h, w, c = img.shape
end_x = min(start_x + patch_width, w)
end_y = min(start_y + patch_height, h)
for i in range(start_x, end_x):
    for j in range(start_y, end_y):
        img[j, i][0] = 255
plt.imshow(img)
plt.show()
```

### 指定区域处理
读取图像并将指定区域的纯白像素改为黄色，其他像素增强绿色通道：
```python
from skimage import io
import matplotlib.pyplot as plt

img = io.imread('x.jpg')
start_x = 2
start_y = 2
patch_width = 6
patch_height = 6
h, w, c = img.shape
end_x = min(start_x + patch_width, w)
end_y = min(start_y + patch_height, h)
for i in range(start_x, end_x):
    for j in range(start_y, end_y):
        r, g, b = img[j, i][0], img[j, i][1], img[j, i][2]
        if r == 0 and g == 0 and b == 0:
            img[j, i] = [255, 255, 0]
        else:
            img[j, i] = [0, 255, 0]
plt.imshow(img)
plt.show()
```

### 星系图像颜色通道处理
使用PIL库分离图像的红色通道并显示：
```python
from PIL import Image
import matplotlib.pyplot as plt

image_path = 'galaxy-full.jpg'
image = Image.open(image_path)
r, g, b = image.split()
r_image = Image.merge('RGB', (r, Image.new('L', r.size), Image.new('L', r.size)))
plt.figure(figsize=(15, 5))
plt.imshow(r_image)
plt.title('Red Channel')
plt.show()
```

使用PIL库分离图像的绿色通道并显示：
```python
from PIL import Image
import matplotlib.pyplot as plt

image_path = 'galaxy-full.jpg'
image = Image.open(image_path)
r, g, b = image.split()
g_image = Image.merge('RGB', (Image.new('L', g.size), g, Image.new('L', g.size)))
plt.figure(figsize=(5, 5))
plt.imshow(g_image)
plt.title('Green Channel')
plt.show()
```

使用PIL库分离图像的蓝色通道并显示：
```python
from PIL import Image
import matplotlib.pyplot as plt

image_path = 'galaxy-full.jpg'
image = Image.open(image_path)
r, g, b = image.split()
b_image = Image.merge('RGB', (Image.new('L', b.size), Image.new('L', b.size), b))
plt.figure(figsize=(15, 5))
plt.imshow(b_image)
plt.title('Blue Channel')
plt.show()
```

### 条纹效果处理
将图像用红绿蓝三种竖状条纹细分处理：
```python
from PIL import Image
import numpy as np
import matplotlib.pyplot as plt

image_path = 'earth.jpg'
image = Image.open(image_path)
image_np = np.array(image)
height, width, _ = image_np.shape
new_image_np = np.zeros_like(image_np)
for i in range(width):
    if i % 3 == 0:
        new_image_np[:, i, 0] = image_np[:, i, 0]
    elif i % 3 == 1:
        new_image_np[:, i, 1] = image_np[:, i, 1]
    else:
        new_image_np[:, i, 2] = image_np[:, i, 2]
new_image = Image.fromarray(new_image_np)
plt.subplot(1, 2, 2)
plt.imshow(new_image)
plt.title('Striped Image')
plt.show()
```

## 使用方法
1、克隆或下载此项目。
2、在项目根目录下运行assignment1_answer来启动应用程序。

## 学习要点
- 如何使用 `scikit-image` 库读取和处理图像
- 如何使用 `matplotlib` 库显示图像
- 如何使用 `Pillow` 库分离和合并图像通道
- 如何通过循环和条件语句处理图像的特定区域


个人信息

    学号: 202352320217
    姓名: 宗军保
    年级: 2023
    专业: 智能科学与技术
    班级: 2 班