### 2023-08-03
## Run bonsai
Try to follow the bonsai exercise 10 to create video which can do tracking
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/2db5b042-bfc4-4cc0-b63f-17affe6320cb)

![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/9550339a-c90c-4c5d-a174-8f933cd996aa)


Run deeplabcut on windows10 from lab

### 2023-08-04
## Run deeplabcut to label the frame
## Try to create labeled video

### 2023-08-07
## Record video, create labeled video
when anaylize video, problems: cannot find .h5 file in the video folder
try to solve the problem, but didn’t find the solution.

### 2023-08-08 
## Find the solution about previous problem
Modify the config file, upload the project on my github and run the same code as dlc demo project.
After get the .csv file, use python to create the tracking picture.

### 2023-08-09
## Run the pipeline
Record the video( Normal WT.OR, Disease WT.K )
Get the labeled video from colab and get the .csv file , use .csv to create a tracking picture by python.

### 2023-08-10
## Adjust the dotsize of the frame
## Retraining the network to make the result more accurate
Yesterday’s result is not satisfied with us ( the problem is the dot is too small so that the result is not accurate.)

### 2023-08-11
## Run the Normal fly project
I set 200000 iterations for my project, but it stopped at 125000.
Then I reinstall the deeplabcut on colab, and run the last step
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/7b501542-250d-4dc1-99b9-fa6290d8e06f)

![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/36f284c0-a5c0-4ae0-b5e3-7dc46eca4f9b)

![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/f9f7ce0e-6faf-4a2e-9ddf-9ba6d189e29f)

The dotsize is very important, my previous labeled video has a very small dot( dotsize is 14 ) !check from the config file , and I don't make a large mount of iteration, almost 10000 like this:
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/f769e388-a0e1-49f2-8131-ef0fa80e01be)

But, after I put the dotsize by 20, and out maxiters to 2000000( finally it just take 125 000 iterations ), looks better than before and be more accurate.
```deeplabcut.train_network(config_file, shuffle=1, displayiters=500,saveiters=1000, maxiters=200000) ```

![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/2b516d80-7a60-40d8-8bac-aa4911534ed7)
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/0d6ddcea-bf5c-4d3a-9f18-fe0b11e5a98a)

Now, what I need to do is to generate the leg tracking picture with python.






## Read the protocol and find how to retrain the network
If we are not satisfied with the accuration of the labeled video, we can add more label frame and train the network named iteration1/2/3, and get a new result.
After that, check the video and be sure that whether to do again.

CALCULATE THE DISTANCE AND SPEED FOR EACH LEG.

finish normal
go to wing
record the lava

### 2023-08-14
## label 100 frames and train 200 000 iteration

change the body part from 7 parts to 6 parts (only legs)
change the dotsize to 18
change the batchsize to 4
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/619fd5a4-56ed-47ca-bafe-d4be803c399e)

label

![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/7697efb2-99ad-4edc-bc1e-d9c4f5879c99)

![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/efdb34eb-29f3-4fe2-a7a2-f3543dcc455b)

after disscusion about the label part it should be like this:
if the leg is not extend, label the first skeletion, if the leg moved, label the part between the second one and the third one
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/f4043ed7-9017-41b2-ba3c-b714ee0a0937)

which kind of the gamma?? normal one or the grey one?
just save

## use the csv fle to calculate the distance and speed of each leg for the file
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/db436b09-d7b8-4931-a309-c18fe123638f)

'''python
## 计算每只腿的运动速度

import pandas as pd
import matplotlib.pyplot as plt

# 读取CSV文件
data = pd.read_csv('N4DLC_resnet50_NAug10shuffle1_129000.csv')

# 提取坐标数据
leftleg1_x = data['leftleg1_x']
leftleg1_y = data['leftleg1_y']
leftleg2_x = data['leftleg2_x']
leftleg2_y = data['leftleg2_y']
leftleg3_x = data['leftleg3_x']
leftleg3_y = data['leftleg3_y']

rightleg1_x = data['rightleg1_x']
rightleg1_y = data['rightleg1_y']
rightleg2_x = data['rightleg2_x']
rightleg2_y = data['rightleg2_y']
rightleg3_x = data['rightleg3_x']
rightleg3_y = data['rightleg3_y']

# 计算总路程
total_distanceL1 = 0
total_distanceL2 = 0
total_distanceL3 = 0
total_distanceR1 = 0
total_distanceR2 = 0
total_distanceR3 = 0

for i in range(1, len(leftleg1_x)):
    dxL1 = leftleg1_x[i] - leftleg1_x[i - 1]
    dyL1 = leftleg1_y[i] - leftleg1_y[i - 1]
    total_distanceL1 += (dxL1**2 + dyL1**2)**0.5

for i in range(1, len(leftleg2_x)):
    dxL2 = leftleg2_x[i] - leftleg2_x[i - 1]
    dyL2 = leftleg2_y[i] - leftleg2_y[i - 1]
    total_distanceL2 += (dxL2**2 + dyL2**2)**0.5
    
for i in range(1, len(leftleg2_x)):
    dxL3 = leftleg3_x[i] - leftleg3_x[i - 1]
    dyL3 = leftleg3_y[i] - leftleg3_y[i - 1]
    total_distanceL3 += (dxL3**2 + dyL3**2)**0.5
    

for i in range(1, len(rightleg1_x)):
    dxR1 = rightleg1_x[i] - rightleg1_x[i - 1]
    dyR1 = rightleg1_y[i] - rightleg1_y[i - 1]
    total_distanceR1 += (dxR1**2 + dyR1**2)**0.5
    
for i in range(1, len(rightleg2_x)):
    dxR2 = rightleg2_x[i] - rightleg2_x[i - 1]
    dyR2 = rightleg2_y[i] - rightleg2_y[i - 1]
    total_distanceR2 += (dxR2**2 + dyR2**2)**0.5
    
for i in range(1, len(rightleg3_x)):
    dxR3 = rightleg3_x[i] - rightleg3_x[i - 1]
    dyR3 = rightleg3_y[i] - rightleg3_y[i - 1]
    total_distanceR3 += (dxR3**2 + dyR3**2)**0.5




# 计算总时间
total_time = 3000

# 计算速度
average_speed_L1 = total_distanceL1 / total_time
average_speed_L2 = total_distanceL2 / total_time
average_speed_L3 = total_distanceL3 / total_time

average_speed_R1 = total_distanceR1 / total_time
average_speed_R2 = total_distanceR2 / total_time
average_speed_R3 = total_distanceR3 / total_time


# print(f"Total DistanceL1: {total_distanceL1}px")
# print(f"Average Speed leftleg1: {average_speed_L1}px/s")
# print(f"Total DistanceL2: {total_distanceL2}px")
# print(f"Average Speed leftleg2: {average_speed_L2}px/s")
# print(f"Total DistanceL3: {total_distanceL3}px")
# print(f"Average Speed leftleg3: {average_speed_L3}px/s")
# print(f"Total DistanceL1: {total_distanceL1}px")

# print(f"Total DistanceR1: {total_distanceR1}px")
# print(f"Average Speed rightleg1: {average_speed_R1}px/s")
# print(f"Total DistanceR2: {total_distanceR2}px")
# print(f"Average Speed rightleg2: {average_speed_R2}px/s")
# print(f"Total DistanceR3: {total_distanceR3}px")
# print(f"Average Speed rightleg3: {average_speed_R3}px/s")



# 创建一个空的DataFrame
columns = ['Leg', 'Total Distance (px)', 'Average Speed (px/s)']
df = pd.DataFrame(columns=columns)

# 你之前计算得到的数据，假设这些数据已经存在
leg_data = [
    ('Left Leg 1', total_distanceL1, average_speed_L1),
    ('Left Leg 2', total_distanceL2, average_speed_L2),
    ('Left Leg 3', total_distanceL3, average_speed_L3),
    ('Right Leg 1', total_distanceR1, average_speed_R1),
    ('Right Leg 2', total_distanceR2, average_speed_R2),
    ('Right Leg 3', total_distanceR3, average_speed_R3)
]

# 将数据逐行添加到DataFrame
for leg, total_distance, average_speed in leg_data:
    df.loc[len(df)] = [leg, total_distance, average_speed]
# 打印自动生成的表格

print(df)```

###  2023-08-16
## train the network to 70000 ( took almost 10 compute units)
during the training time, I met the 'busy' situation as most of people, I chose to wait until it showed the issue like this:
https://github.com/googlecolab/colabtools/issues/3441
## analyze the video and get the .csv file (2 compute units) 
Then I chose to contiue the next step, analyze the video, it looks like good, so I add the other videos (3 normal and 4 disease)
<img width="1415" alt="截屏2023-08-17 11 00 20" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/61bd9187-1d4c-4b71-876e-4d6172c504b8">
<img width="1406" alt="截屏2023-08-17 11 01 35" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/7224ba04-f8e7-425f-8187-e1799bb86184">

Use each video generate the picture of six legs (200 rows)
<img width="1470" alt="截屏2023-08-16 22 47 54" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/0f7f73f5-8f99-4b29-824e-22eddea872ad">

## use the .csv file to calcute the distance and the speed for both kind of file
1. adjust the file ( delete the scorer and likelihood, delete the two rows)
   <img width="1389" alt="截屏2023-08-16 18 16 27" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/62ef868b-ef97-44d4-8869-ae274533837e">
2. merge the file for comparison


### 2023-08-17
## calculate the distance and speed for each video
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/b0ff954d-eadc-4439-a132-220d81449a2f)

Then merge leftleg and rightleg to 'leg'
<img width="1235" alt="截屏2023-08-17 16 02 14" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/64b884c7-ec37-4ccf-86e6-e8bf84833091">

## Generate the plot (learn SEM standard error mean)

![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/9c7a550a-49d7-4e87-ad2d-769b1251ec3d)


## train wing network (84.13 compute unites)
analyze video
generate video (74.43 computer unites)
check the video, it's accurate.
<img width="640" alt="截屏2023-08-17 16 29 05" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/00ed9f7d-68b9-4a46-b758-49a8fc035c9c">
<img width="503" alt="截屏2023-08-17 16 29 24" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/3f96085b-7ebc-47c3-a6e6-641e6c92c494">
<img width="526" alt="截屏2023-08-17 16 29 46" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/f4279632-cc29-4d7a-8576-0db43cec220d">
<img width="559" alt="截屏2023-08-17 16 30 18" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/dee5b70f-63e1-410a-b98f-fe930cf75991">

## Then analyze the other videos (72.64 compute unites)

## Generate the picture of each wing
![image](https://github.com/Ruoqi277/Internship-DLC/assets/132852026/3859b60c-8807-4806-97a7-38d105525b72)

## Calculate the Distance and speed

### 2023-08-18
## record the larva video (group 1 and group 2)
label the frames

## upload Larva project folder on my colab drive start training and analyze (71.96 compute unites)
train the network
<img width="1447" alt="截屏2023-08-18 14 48 53" src="https://github.com/Ruoqi277/Internship-DLC/assets/132852026/58dc22f5-dbeb-4716-9bcf-26f688977f37">
50.42 training

## evaluate the network
## anayze the video 50.01 compute unites
check the tracking picture, there is some special dot for the tail, so we only choose the head part for tracking
固定每一张图的尺寸。
## continue to calculate the wing distance and speed
















