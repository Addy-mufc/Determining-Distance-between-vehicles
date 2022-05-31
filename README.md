# Determining-Distance-between-vehicles

In this project, we are using the YOLOv4 framework to identify a vehicle in an image or a video (a sequence of images). This serves as the first stage in the development of this project, which also enables us to identify the future steps to be worked on to improve the project. It is also essential in the next stage,. i.e, Deep SORT, where we track the identified vehicle.

The Distance metric is the distance between the adjacent vehicles or objects and the Autonomous Vehicle itself. This metric is necessary because it not only helps in determining the speed of the vehicle but also improves the prediction of the vehicle. It is also essential in manoeuvring the Autonomous Vehicle and warning it of possible crashes, ultimately leading to collision avoidance.
 
There have been several attempts to determine the distance between the Autonomous vehicle and the neighbouring vehicles. Some try to use vision-based methods by using a camera fit to a car and identify the number plate fit to the car. As number plates use standardized fonts, this size is related to the distance between the camera and the preceding vehicle. In current automotive research, companies mainly focus on two methodologies in collision detection using sensors - radar-based and vision-based . Radar-based collision detection has a transceiver installed in front of the host vehicle. It transmits waves, such as infra-red or ultrasonic, receives the reflections. The system calculates the reflected wavelength and hence finds the distance between the host and the target vehicle. The radar-based systems have limitations such as: being unable to detect whether the target is moving or stationary, also the angle of the infra-red beam is narrower over longer distances.
 
The proposed method to determine the distance of the nearby car by using a few parameters- the area of the bounding box and the number of pixels between the centre of the bottom edge of the bounding box and the centre of the bottom of the screen. The bottom of the screen is taken because the bonnet/hood of the car is present at the bottom of the screen. This is done in coordination with YOLOv4 and Deep SORT. YOLOv4 provides the coordinates of the bounding box which is then used to calculate the area of the bounding box along with the number of pixels between the centre of the bottom edge of the bounding box and the centre of the bottom of the screen.
 
Now using these two parameters, the distance between the Autonomous Vehicle and the neighbouring vehicle can be estimated. For this, we decided to use Multiple Linear Regression(MLR).
 
Multiple linear regression (MLR) is a statistical technique that uses several independent variables to predict the outcome of a dependent variable. The goal of multiple linear regression is to model the linear relationship between the explanatory (independent) variables and response (dependent) variables. In essence, multiple regression is the extension of ordinary least-squares (OLS) regression or Linear Regression because it involves more than one independent variable.
 
y=β0+β1xi1+β2xi2                                              
where 
y= Distance between Autonomous Vehicle and Neighbouring Vehicle
β0= Constant
β1x1= Regression Coefficient β1 w.r.t Area
β2x2= Regression Coefficient β2 w.r.t number of pixels 

The dependent variable will be the distance between the neighbouring vehicle and the Autonomous Vehicle while the dependent variables will be the area of the bounding box and number of pixels between the centre of the bottom edge of the bounding box and the centre of the bottom of the screen. Once the Linear Regression model is trained, it is able to predict the distance.


We conducted an experiment by taking photos of the same vehicle at different distances. These images were then given as input to the YOLOv4 algorithm to identify the vehicle and draw the bounding boxes around the identified vehicle. The distances at which the images were taken are 1 metre, 5 metres and 10 metres.

![image](https://user-images.githubusercontent.com/75781787/171103987-252abfcf-0b87-4ab7-9163-f5155c50d118.png)

In this Figure, when the car is at a distance of 1 metre from the camera, the area of the bounding box is 4380160 pixels. 


![image](https://user-images.githubusercontent.com/75781787/171104055-9e32d822-8128-4c81-a6a5-da5336db0de3.png)

In this Figure, when the car is at a distance of 5 metres from the camera, the area of the bounding box is 614250 pixels. 


![image](https://user-images.githubusercontent.com/75781787/171104075-88b8c16b-ecda-478c-abc2-3d793d68ea1c.png)

In this figure, when the car is at a distance of 5 metres from the camera, the area of the bounding box is 199360 pixels.

![image](https://user-images.githubusercontent.com/75781787/171104275-52236184-8914-4c23-abcf-697aaa98fd56.png)



It can be clearly observed that as the vehicle moves further away from the camera, the area of the bounding box reduces. This means that Area of the bounding box is inversely proportional to the distance between the camera and the Vehicle.
 
![image](https://user-images.githubusercontent.com/75781787/171104371-18e812b2-ae17-4c70-af27-0a8a662caa10.png)


The dataset train_test is created by using various videos that were shot at different distances (1 metre, 2 metres, 3 metres and so on until 5 metres) and different angles. YOLOv4 and Deep SORT frameworks were applied on these videos to obtain the maximum and the minimum coordinates. These coordinates were used to determine the area of the bounding box by calculating the height and width. The dataset consists of three parameters: Area, Gap, Distance and over 9000 datapoints. This labelled dataset is used to train the Linear Regression model for determining the distance between the camera(Autonomous Vehicle) and the neighbouring vehicle.



Outputs can be seen as follows:




https://user-images.githubusercontent.com/75781787/171106493-97eae686-0808-4f7c-97ef-2903e4cb2f5e.mp4




https://user-images.githubusercontent.com/75781787/171106496-4ae95309-d8ba-4c1a-a9cd-99e07efa3285.mp4


