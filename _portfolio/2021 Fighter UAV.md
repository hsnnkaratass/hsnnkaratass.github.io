---
title: "2021 Teknofest Fighter UAV Competition"
excerpt: "In 2021, I actively participated in the Fighter UAV Competition organized as part of the TEKNOFEST Technology competitions. Tasked with  developing a UAV-GCS system with the “Autonomous Dogfight” capability. In the given area, the developed system must have autonomous takeoff, flight and landing. Only allowed sensor for the autonomous dogfight is camera. As a member of my team, our objective was to comprehend and develop the autonomous dogfight algorithms and explore their potential applications in military domains.<br/><img src='/images/FU.png' width='600' height='450'>"
collection: portfolio
---


## About the Competition

The Fighter UAV Competition, organized within the TEKNOFEST Technology competitions, focuses mainly on Autonomous Dogfight, a technology gaining increasing importance with developing UAV's. In parallel with developments in technology, Unmanned Aerial Vehicles (UAVs) are continuously improving their operational capabilities and gaining more autonomy. In this context, the goal is to equip UAVs, which already have a high level of autonomy, with the ability to engage in dogfights similar to those conducted by fighter jets. The competition showcases the practical functionality of these algorithms by deploying Swarm UAVs in real-world conditions. Key objectives include understanding how software algorithms for swarming UAVs operate, exploring the technology's potential in civil and military applications, and encouraging young talents in this field. Given the transformative potential of Swarm UAVs in daily life and defense strategies, the competition aims to contribute to the technology's development.

<p align="center">
  <img src="/images/savasan.png" alt="Figure 1 - 2021 Fighter UAV Competition"/>
</p>

## Autonomous Dogfight Mission

In order to fulfill the autonomous dogfight mission, according to rules, teams must conduct some requirements. Firstly, only allowed sensor is camera. No other sensors like radar cannot be used. Also, gimbal cannot be used for changing the direction of the camera. Secondly, the shot is achieved by the UAV performing the lock-on by taking the image of the opponent UAV into its own camera image. In order for the interlock to occur, the moving rival UAV must be kept within a square region in the center of the camera image for at least 4 seconds.  The size of this square area is as shown in Figure 2. At the same time, the image of the opponent UAV must cover at least 5% of the screen image on at least one of the horizontal and vertical axes (see Figure 2).

<p align="center">
  <img src="/images/rectangle.png" alt="Figure 2 - Sample Lock Area"/>
</p>


## My Responsibilities

I have responsibilities on various fields as my teammates. In my first year at the team I worked in the computer vision sub-unit, we have performed tasks such as creating algorithm architectures that utilize artificial neural networks for object detection and tracking, collecting the necessary data to train these networks, duplicating it, and extracting relative positional vectors of detected objects using stereo vision. I worked mainly on stereo vision, data preparation and augmentation for the training and test parts. Other than software, I worked with UAV avionics, wifi and telemetry communications,  power distribution of avionics. Furthermore, I gained experience as a Ground Control Station and UAV-1 pilot.

### Data Preparation and Model Training

We developed an object detection algorithm using Res-Net structure. We used Resnet-18, because we need to detect only UAV's and the model should be relatively light. We altered the last the layer of the model to give five different outputs. First output gives 1 or 0 according to whether there is a UAV or not in the scene. If there is, last four output gives the rectangle surruonding the UAV. We implemented it using Pytorch and the ResNet structure can be seen in the Figure 1. We selected ResNet because of the ... 

<p align="center">
  <img src="/images/resnet18.png" alt="Figure 1 - ResNet18 Structure"/>
</p>

<p align="center">
  <em>Figure 1 - ResNet18 Structure</em>
</p>

For the training part, Complete Intersection of Union (CIOU) was selected because it is more suitable for our case. It does not only chechk the intersection over union of the ground truth and output, it also takes into account the distance between the centers of the predicted and ground truth bounding boxes. For the optimization part, widely used Adam optimizer was selected. 

After developing neural network archtitecture, we dive into to the data prepration part. Training and test data are one of the most important things for the accuracy of the model. So, we give importance on dataset creation. We gathered 10.000 labelled images from the "RC Chasing" videos from YouTube. In order to avoid bias and variance on our model, we used detailed labelling. Images were labelled according to seven categories in the Table 1. 

*Table-1. Categories of the Labels*

|   Parameter               | Example Parameter Type        |
| --------------            | ------------------ |
| Object Type               | RC, Commercial Plane    |
| Background Type           | Mountain, Forest, City, Asphalt  |
| Cloudiness Rate           | Cloudless, Very, Partly Cloudy  |
| Day Status                | Morning, Afternoon, Evening     |
| Relative Camera Position  | Lower, Top, Side                |
| Colour of Object          | Black, White, Red ...           |
| Size of Object            | Small, Big, Middle |

In the competition area, we knew that the background was mostly mountain. So the mountain type background had an important weight in the distribution. Other parameters was also be set according to competition area conditions. One example from our dataset can be seen in figure 2. Here we labelled them in Turkish and the meanings are; "rc = radio controlled", "asfalt = aspalth", "azBulutlu = partly cloudy", "aksam = evening", "alt = from lower", "siyah = black", "orta = middle size".

<p align="center">
  <img src="/images/label.png" alt="Figure 2 - Example Labelling"/>
</p>

<p align="center">
  <em>Figure 2 - Example Labelling</em>
</p>

We gathered 10.000 labeled raw images like the Figure 2, in order to increase the image number and diversity, we applied augmentation techniques like flipping, rotating and random cropping. After augmentation, finally we got 110.000 labelled images for training.

### Stereo Vision

Autonomous dogfight requires our system to know the relative locaiton of the UAV that will be tracked. After object detection part, we are going to get the relative locaiton of the target in 2 dimensions. So we are going to control the pitch and roll movements. In order to control the speed, one possible choice is bounding box size. If it is small, make the UAV nove faster or vice versa. However, for some cases, we observed that the bounding box that model predicts does not fit the UAV. So, we decided to get the exact 3D relative location of the tracked UAV according to our UAV's locaiton and create a vector from us to tracked UAV. Then speed, pitch and roll will be controled according to that vector. 

For stereo vision, we developed algorithm based on keypoint detection from two cameras and matching the detected keypoints. After matching the keypoints, from their pixel locaitons on the camera screen, the distance of the rival UAV can be found from the basic triangle equations. 
#todo resim ekle
For keypoint detection, we used superpoint algorithm, it is .... 
for matching the detected keypoints, we used lightglue. it is .....

Although, algorithms were mostly ready for the task, the mechnaical problems arrived.... 

## Competition and Results

### Preparation

sayısız test 
adım adım sistem testleri
test çeklistleri
ikinci UAV
başarılamamış olması

Our journey towards the AUVSI SUAS 2022 competition was an intensive and rewarding experience that spanned eight months. Collaborating across disciplines—Aerospace, Mechanical, Metallurgical, and Materials Engineering—my team and I delved into the intricacies of designing, building, and operating unmanned aerial vehicles (UAVs). Despite the challenges posed by our demanding academic schedules, the collaboration proved to be a joyous yet demanding endeavor. The competition provided a platform for us to translate theoretical knowledge into practical applications, pushing the boundaries of our understanding. Through rigorous testing of our UAV, I gained valuable insights and practical experience that enhanced my learning.

### Competition Details

**Location:** The Fighter UAV 2021 competition took place from August 15th to 20th at Bursa Yunuseli Regional Airport.

**Mission Testing:** As a responsible member during the mission testing phase, we encountered some challenges, particularly with wifi connections, which sometimes affected the image transfer to the GCS. However, despite these hurdles, the mission test provided valnurable experince for us.

**Flight Video:** You can witness our flight video during the competition.

<iframe width="560" height="315" src="https://www.youtube.com/embed/eu7qqW2X3FY" frameborder="0" allowfullscreen></iframe>

### Results

Teams participating in the Fighter UAV 2021 competition were evaluated based on Mission Rank, Flight Proveness Video, and Critical Design Report Ranking, ultimately contributing to their Overall Rank. Also, there were judge special awards. Here are our team's rankings:

- **Critical Design Report Rank:** 1
- **Mission Demonstration Rank:** 2
- **The Most Original Software Award**

The Fighter UAV Competition has been held since 2019; however, because of the task difficulty no team was able to fulfill the competition main task which was guiding a rival UAV within a distance specified in the competition rules and not removing it from the camera view for 4 seconds. We were one of the first the first and only three teams that fulfill the competition tasks. After 2021, up to now, still the autonomous dogfight mission could not be fulfilled. 

You can check the detailed rankings [here](https://www.teknofest.org/tr/yarismalar/savasan-iha-yarismasi/). Additionally, our Flight Readiness Review video is available for viewing below.

<iframe width="560" height="315" src="https://www.youtube.com/embed/zmkGAIbsrh4" frameborder="0" allowfullscreen></iframe>


## Important Reminder

Since this was a team project, I cannot share codes without permission of my team 😞.
