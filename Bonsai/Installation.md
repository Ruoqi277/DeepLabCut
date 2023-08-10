# Bonsai
Bonsaï的安装和使用

## 1.Go to the website https://bonsai-rx.org/docs/articles/installation.html

I downloaded the installer version and launched.

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/f3ce5ef5-7a20-4263-9af4-416f247b31d8)

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/f7a17b7a-f7ad-4d47-96ef-143225ceaddb)

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/8e294523-e31b-4765-b696-82412aa55bc6)

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/1d0bf053-b7d9-444f-a63d-fe397b4214cd)

## 2.Follow the Package Manager from the website.
Install "Starter Pack"

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/5f06470c-d902-402c-9394-f87db539494f)

Then we can see Workflow editor
![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/86269b42-a9e8-4c12-b7c5-50033b881f34)

## Folowing are my exercise from Acquisition and Tracking https://bonsai-rx.org/docs/tutorials/acquisition.html

### Exercise 9

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/0b8ed052-d049-41d2-8f5e-0669671b5372)

There has a Build Error:

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/2440b6ba-cf2f-4a94-963a-31a02fa0f1d6)

ConvertColor converts the image from BGR colour space to the Hue-Saturation-Value(HSV) color space.

Here are some information about HSV: https://en.wikipedia.org/wiki/HSL_and_HSV

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/eb282d45-e73b-4748-ba5a-0c96ede20a6d)

Error

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/b05b577b-fdf4-4d74-b3df-c6c3360d83c1)

### Exercise 10

![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/35b152f3-3188-49b0-83c9-c17669b5927f)

FindContours transform:
该运算符追踪黑白图像中所有对象的轮廓。对象被定义为连接的白色像素的区域

BinaryRegionAnalysis:
计算所有检测到的轮廓的面积、质心和方向

LargestBinaryRegin:
提取图像中检测到的最大对象

Centroid:
Select the ConnectedComponent > Centroid field of the largest binary region using the context menu.
使用上下文菜单选择最大二进制区域的ConnectedComponent>字段。Centroid

CswWriter:
使用水槽记录质心的位置

### Q1 What's filename?
The name of the output CSV file 
csv是纯文本文件， 每项数据用逗号分开（标准英文逗号）它可以被Excel打开
需要用引号把文件名括起来
#### CRC32校验值 整个CSV文件的精髓
假如你收到一张图片，名字是0001.jpg，你知道它是jojo子集的一张，但不知道具体是哪一张
这个时候可以先用软件得到图片的大小和CRC值，然后软件会在CSV文件里找到一行jojo1001.jpg，大小和CRC都符合，软件就会认为这张图片的原名是jojo1001.jpg，接着把文件名字更改为jojo1001.jpg
![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/9f575ef9-c68d-4715-9647-58b4191979aa)

第一个文件命名为demo
![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/2f01b432-a5c3-4c56-b113-37d769acf8e5)
![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/72a16d47-f7e9-4029-ae03-dda5edd7baef)
![image](https://github.com/Ruoqi277/Bonsai/assets/132852026/f9faad91-0211-4920-af77-8659db8a4ea5)















