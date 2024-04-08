---
title: "2021 Teknofest Fighter UAV Competition"
excerpt: "The Fighter UAV Competition, organized within the TEKNOFEST Technology competitions, focuses mainly on Autonomous Dogfight, a technology gaining increasing importance with developing UAV's. In parallel with developments in technology, Unmanned Aerial Vehicles (UAVs) are continuously improving their operational capabilities and gaining more autonomy. In this context, the goal is to equip UAVs, which already have a high level of autonomy, with the ability to engage in dogfights similar to those conducted by fighter jets. The competition showcases the practical functionality of these algorithms by deploying Swarm UAVs in real-world conditions. Key objectives include understanding how software algorithms for swarming UAVs operate, exploring the technology's potential in civil and military applications, and encouraging young talents in this field. Given the transformative potential of Swarm UAVs in daily life and defense strategies, the competition aims to contribute to the technology's development.

<br/><img src='/images/FU.png' width='600' height='450'>"
collection: portfolio
---

## About the Competition

In 2021, I actively participated in the Fighter UAV Competition organized as part of the TEKNOFEST Technology competitions. Tasked with  developing a UAV-GCS system with the “Autonomous Dogfight” capability. In the given area, the developed system must have autonomous takeoff, flight and landing capabilities. As a member of my team, our objective was to comprehend and develop the autonomous dogfight algorithms and explore their potential applications in military domains. In order to accomplish the autonomous dogfight, me and my team put a valuable effort. Below you can find the competition rules and my responsibilities.

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

We developed an object detection algorithm using Res-Net structure. We used Resnet-18, because we need to detect only UAV's and the model should be relatively light. We altered the last the layer of the model to give five different outputs. First output gives 1 or 0 according to whether there is a UAV or not in the scene. If there is, last four output gives the rectangle surruonding the UAV. We implemented it using Pytorch and the ResNet structure can be seen in the Figure 1. We selected ResNet, because, when compared to ResNet-34, ResNet-50, and other deep learning architectures, ResNet-18 is relatively shallow. It is made up of 18 layers, including convolutional, pooling, fully connected, and shortcut connections. In comparison to deeper models, the reduced depth facilitates training and allows for faster convergence. Also, the concept of residual learning enables the network to learn residual mappings, i.e., the difference between the input and output of a layer. This facilitates the training of deeper networks and helps alleviate the vanishing gradient problem. 

<p align="center">
  <img src="/images/resnet18.png" alt="Figure 3 - ResNet18 Structure"/>
</p>

<p align="center">
  <em>Figure 3 - ResNet18 Structure</em>
</p>

For the training part, as a loss function Complete Intersection of Union (CIOU) was selected because it is more suitable for our case. It does not only chechk the intersection over union of the ground truth and output, it also takes into account the distance between the centers of the predicted and ground truth bounding boxes. After using CIOU we observed that the accuracy of the model increased and the training time was decreased. For the optimization part, widely used Adam optimizer was selected. 

After developing neural network archtitecture, we dive into to the data prepration part. We know that the training and test data are one of the most important things for the accuracy of the model. So, we give importance on dataset creation. We gathered 10.000 labelled images from the "RC Chasing" videos from YouTube. In order to avoid bias and variance on our model, we used detailed labelling. Images were labelled according to seven categories in the Table 1. 

*Table-1. Categories of the Labels*

|   Parameter               | Example Parameter Type        |
| --------------            | ------------------ |
| Object Type               | RC, Commercial Plane    |
| Background Type           | Mountain, Forest, City, Asphalt  |
| Cloudiness Rate           | Cloudless, Very, Partly Cloudy  |
| Day Status                | Morning, Noon, Afternoon, Evening     |
| Relative Camera Position  | Lower, Top, Left -Right Side          |
| Colour of Object          | Black, White, Red ...           |
| Size of Object            | Small, Big, Middle |

In the competition area, we knew that the background was mostly mountain. So the mountain type background had an important weight in the distribution. Other parameters was also be set according to competition area conditions. One example from our dataset can be seen in Figure 4. Here we labelled the image as "rc = radio controlled", "mountain", "cloudless", "Noon", "Top", "yellow", "middle".

<p align="center">
  <img src="/images/data.png" alt="Figure 4 - Example Labelling"/>
</p>

<p align="center">
  <em>Figure 4 - Example Labelling</em>
</p>

We gathered 10.000 labeled raw images like the Figure 4, in order to increase the image number and diversity, we applied augmentation techniques like flipping, rotating and random cropping. After augmentation, finally we got 110.000 labelled images for training. 

Finally, after training the developed dataset, we conducted inference using the Nvidia Xavier-NX platform, which yielded a commendable performance of 70 frames per second (FPS). This demonstrates the efficiency of the deployed detection algorithm in real-time object detection. Moreover, the accuracy of the model showcased promising results, indicating its effectiveness in accurately identifying objects. The achieved FPS and accuracy metrics serve as strong indicators of the algorithm's capability to handle real-world scenarios and contribute to the overall success of the dogfight mission.

### Stereo Vision

Autonomous dogfight requires our system to know the relative locaiton of the UAV that will be tracked. After object detection part, we are going to get the relative locaiton of the target in 2 dimensions. So we are going to control the pitch and roll movements. In order to control the speed, one possible choice is bounding box size. If it is small, make the UAV nove faster or vice versa. However, for some cases, we observed that the bounding box that model predicts does not fit the UAV. So, we decided to get the exact 3D relative location of the tracked UAV according to our UAV's locaiton and create a vector from us to tracked UAV. Then speed, pitch and roll will be controled according to that vector. 

For stereo vision, we developed algorithm based on keypoint detection from two cameras and matching the detected keypoints. After matching the keypoints, from their pixel locaitons on the camera screen, the distance of the rival UAV can be found from the basic triangle equations as can be seen from Figure 5. 

<p align="center">
  <img src="/images/stereooo.png" alt="Figure 5 - Stereo Triangle"/>
</p>

<p align="center">
  <em>Figure 5 - Stereo Triangle</em>
</p>


For keypoint detection, we used superpoint algorithm, it is a deep learning-based algorithm that finds keypoints and their corresponding descriptors in the image. A convolutional neural network architecture designed for interest point detection and description is trained using a self-supervised domain adaptation framework called Homographic Adaptation. This framework enables the network to adapt and learn from different domains without explicit supervision. It consists of three parts as can be seen from the Figure 6, namely; Interest point pre-training, Interest point self-labeling, and Joint training. In the first part, the algorithm was trained with synthetic datasets for corner detection. After training with a lot of shapes in various orientations, the algorithm was able to detect corners more accurate than past stateof-the-art algorithms like Shi and Harris cornet detection.

<p align="center">
  <img src="/images/sup.png" alt="Figure 6 - Superpoint Architecture"/>
</p>

<p align="center">
  <em>Figure 6 - Superpoint Architecture</em>
</p>

However, it was just trained on a synthetic dataset, and its performance on real images could not be enough for the task. To make it robust on real-world images, the second part “Homographic Adaptation” is used. The goal is to adapt an initial interest point function, denoted as fθ(·), to be more effective in detecting interest points in a given target domain. The method operates in a self-supervised paradigm, where a large set of images from the target domain is used that images is unlabeled images. The main part of the method is the application of random homographies to warped copies of the input image can be seen in Figure 7. 

<p align="center">
  <img src="/images/homography.png" alt="Figure 7 - Homographic Adaptation"/>
</p>

<p align="center">
  <em>Figure 7 - Homographic Adaptation</em>
</p>

The formulation of the method involves representing the initial interest point function as fθ(·), the input image as I, the resulting interest points as x, and a random homography as H. The ideal interest point operator should be covariant concerning holographic, meaning that the output should transform with the input. In other words, if H is a homography, then Hx should be equal to fθ(H(I)). However, a detector may not be perfectly covariant in practice, and different homographies can result in different interest points. The Homographic Adaptation process aims to address this by performing an empirical sum over a large sample of random homographies. The aggregation of samples gives rise to a new14 and improved interest point detector, denoted as Fˆ(·), which is more effective at detecting
interest points. The equation for the adapted detector is:

<p align="center">
  <img src="/images/equation.png" alt="Figure 8 - Adapted Detector Equation"/>
</p>

<p align="center">
  <em>Figure 8 - Adapted Detector Equation</em>
</p>

After finding the keypoints also in the real-world images, the last task is to find the correspondence descriptors for keypoints. SuperPoint algorithm does this job in the single forward-pass network in real-time. Its architecture can be seen in Figure 9. The model utilizes a shared encoder that takes the input image and reduces its dimensionality through pooling. This encoder is responsible for processing the image and extracting meaningful features. After the encoder, the model diverges into two separate decoders "heads". Each head learns task-specific weights for a particular objective: one head focuses on detecting interest points, while the other head focuses on describing those interest points.

<p align="center">
  <img src="/images/desc.png" alt="Figure 9 - Descriptor Finding Architecture"/>
</p>

<p align="center">
  <em>Figure 9 - Descriptor Finding Architecture</em>
</p>

For matching the detected keypoints, we used superglue algorithm. It basicly tries to find the matching parameters of the decriptors and uses negative log-likelihood as a loss function. 

Although, algorithms were mostly ready for the task, the mechnaical problems arrived. We couldn't stabilize the two cameras apart from each other. We tried to put them under the wings but there were shaking at the wings and the image couldn't taken properly. Also, we had lots of tests to prove the accuracy of the object detection algorithm. So, we decided to control the speed of the UAV from bounding box size. However, working on stereo vision task gave me valuable experiences. 

## Competition and Results

### Preparation

Over the course of ten months, we had a demanding and fulfilling experience getting ready for the Fighter UAV Competition. Working together across disciplines, my team and I explored the complexities involved in creating, assembling, and using unmanned aerial vehicles (UAVs). The partnership turned out to be a joyful but challenging undertaking, despite the difficulties brought on by our demanding academic schedules and the pandemic. By pushing the limits of our understanding, the competition gave us a platform to apply theoretical knowledge in real-world situations. We put our UAV through a rigorous testing process that gave me insightful knowledge and real-world experience that improved my learning. 

In our endeavor to undertake the mission flight, we meticulously conducted numerous system identification and tuning tests. Throughout the progression from the initial flight to the comprehensive mission test, we encountered a multitude of challenges and obstacles, including the unforeseen impact of the pandemic. Nevertheless, undeterred by these adversities, we persevered and remained resolute in our efforts to achieve a historic milestone – becoming the first team in the history of Teknofest to successfully accomplish the feat of Autonomous Dogfight.


### Competition Details

**Location:** The Fighter UAV 2021 competition took place from August 15th to 20th at Bursa Yunuseli Regional Airport.

**Mission Testing:** As a responsible member during the mission testing phase, we encountered some challenges, particularly with wifi connections, which sometimes affected the image transfer to the GCS. However, despite these hurdles, the mission test provided valnurable experince for us.

**Flight Video:** You can witness some part of the our flight video during the competition.

<iframe width="560" height="315" src="https://www.youtube.com/embed/QpyCNWbW3N8?si=cOkTOUCVD-4KVa2-" frameborder="0" allowfullscreen></iframe>
### Results

Teams participating in the Fighter UAV 2021 competition were evaluated based on Mission Rank, Flight Proveness Video, and Critical Design Report Ranking, ultimately contributing to their Overall Rank. Also, there were judge special awards. Here are our team's rankings:

- **Critical Design Report Rank:** 1
- **Mission Demonstration Rank:** 2
- **The Most Original Software Award**

After dedicating considerable effort and perseverance, our team's hard work paid off as we secured the honorable second place in the competition. Additionally, we were recognized with the esteemed Most Original Software Award by the judge committee, acknowledging our innovative approach in developing the software component. Most significantly, we achieved a remarkable milestone by being among the first teams to successfully accomplish the autonomous dogfight, solidifying our position as pioneers in this groundbreaking field.

<p align="center">
  <img src="/images/odul.jpg" alt="Figure 10 - Awards"/>
</p>

<p align="center">
  <em>Figure 10 - Awards </em>
</p>

The Fighter UAV Competition, initiated in 2019, has posed a significant challenge to participating teams. The main objective of the competition was to guide a rival UAV while maintaining its presence within the camera view for a continuous duration of 4 seconds, as stipulated by the competition rules. Despite several attempts by numerous teams, no successful completion of this task was achieved until our team, along with two other teams, emerged as pioneers by accomplishing the competition objectives. Remarkably, since 2021 until the present, the mission of autonomous dogfighting remains unfulfilled, signifying the complexity and demanding nature of this particular endeavor.

You can check the detailed rankings [here](https://www.teknofest.org/tr/yarismalar/savasan-iha-yarismasi/). Additionally, our System Identification video is available for viewing below. Video is in Turkish, if needed subtitles can be used. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/7RJkg5f8BT4?si=3nTQHWU7Y4v6-jUR" frameborder="0" allowfullscreen></iframe>

## Important Reminder

Since this was a team project, I cannot share codes without permission of my team 😞.