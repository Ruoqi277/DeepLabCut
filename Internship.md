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
