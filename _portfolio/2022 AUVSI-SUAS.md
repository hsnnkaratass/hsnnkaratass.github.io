---
title: "AUVSI SUAS 2022 Competition"
excerpt: "AUVSI SUAS is an annual competition that challenges student teams to design, build, and operate unmanned aerial vehicles (UAVs or drones). The competition typically involves a series of missions that test the capabilities of the teams' autonomous systems. These missions often include tasks such as autonomous flight, target identification, and payload delivery.<br/><img src='/images/kesekci.jpg' width='600' height='450'>"
collection: portfolio
---

## Competition Tasks

You can get more information about the competition from [this link](https://suas-competition.org/competitions). Also you can watch the SUAS Competition trailer from the video below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/XupkKjTokhM?si=vlh4QzVcCpCjQcc7" frameborder="0" allowfullscreen></iframe>


### Autonomous Flight

In the Autonomous Flight mission, teams are tasked with ensuring their Unmanned Aerial Systems (UAS) can fly autonomously for a minimum of 3 minutes. The transition between autonomous and manual mode must be communicated to the safety judge, with a focus on precise waypoint navigation.

### Obstacle Avoidance

Obstacle Avoidance is crucial for UAS integration into airspace. Teams need to showcase effective obstacle avoidance capabilities while navigating both stationary obstacles and other UAS within shared airspace.

### Object Detection, Classification, and Localization

In this mission, teams must demonstrate their UAS's ability to detect, classify, and accurately locate objects. Standard and emergent objects, with specific characteristics, need to be identified, with telemetry uploaded at 1Hz for effective object detection.

### Mapping

The Mapping mission requires teams to generate high-quality imagery maps conforming to the Web Mercator projection. The evaluation focuses on map coverage, accuracy, and overall quality.

### Air Drop

Teams participating in the Air Drop mission are challenged to precision-drop a payload and design a Unmanned Ground Vehicle (UGV) capable of carrying a standard water bottle. Points are awarded for accuracy in both the drop and subsequent drive to a specified location.

## My Responsibilities

I served as the coordinator of the Software and Electronics Subteam, encompassing various responsibilities within the project. Within the electronic subteam, our focus was on developing an avionic system to ensure the proper functioning of our unmanned aerial vehicle (UAV) named 'KESEKCI'. Working alongside the software subteam, our objective was to create algorithms that would enable autonomous takeoff, flight, and landing capabilities for the UAV.

Our efforts extended beyond basic functionality, as we incorporated advanced features such as mapping capabilities, object detection, air drop functionality, and static path planning to avoid obstacles within the designated area. Specifically, my primary software-related responsibility entailed the development of a computer vision algorithm designed to identify and classify emergent and standard objects. Additionally, I was tasked with the creation of test plans and the distribution of tasks to facilitate test preparation.

As part of our work at ANATEK, we conducted numerous system identification and tuning tests, spanning from the initial flight trials to comprehensive mission tests.

### Object Detection Classification and Localization

As its name suggests, object detection, classification, and localization are three principal components. We planned to complete the sections independently. In the competition area, there were some figures in different shapes like rectangle, triangle and pentagon. All of them are in different colours and inside the shapes, there was number or letter like "1", "A", "B". In order to detect this shapes, we decided to use classical algorithms like "Blob Detection".   

#### Region of Interest Detection

During the region of interest (ROI) detection stage, captured images undergo pre-processing to mitigate undesired distortions and enhance the frame's features, thus optimizing the subsequent blob detection algorithm. This pre-processing involves rescaling the image to a standardized size and applying Gaussian and Otsu blur processing techniques. Rescaling ensures consistent dimensions across images, facilitating consistent blob detection results. Gaussian blur reduces noise and smooths irregularities, enhancing the image's quality. Otsu blur processing utilizes an automatic thresholding algorithm to segment the ROI, distinguishing blobs from the background. The combined application of these techniques improves the blob detection algorithm's performance by suppressing distortions, reducing noise, and enhancing features within the ROI. 

Following the preprocessing stage, we employed Blob Detection, a computer vision technique designed to identify and locate regions of interest (blobs) within an image. This technique operates by analyzing the pixel intensity or color distribution in an image, enabling the differentiation of regions that deviate significantly from their surroundings and labeling them as foreground objects. In our specific scenario, which involves a regional airport surrounded by trees, Blob Detection proves particularly useful for distinguishing objects of interest amidst the potential presence of competing elements. Below you can see our test results using the Blob Detection Algorithm. 


<p align="center">
  <img src="/images/ROI.gif" alt="Figure 1 - ROI Detection"/>
</p>

<p align="center">
  <em>Figure 1 - ROI Detection</em>
</p>


#### Classification

In the context of object classification, several features need to be determined, including color, shape, and alphanumeric information present within the object. To address the color aspect, the average pixel values across the red, green, and blue (RGB) channels of the object's pixels are computed. By analyzing the resulting average value, it is possible to assign the object to a specific color range based on predefined thresholds. Shape determination is accomplished through the utilization of the Hu moment technique. Prior to shape analysis, an image preprocessing step is applied to identify the region of interest (ROI) containing the object. Subsequently, the Hu moments of the object are calculated, capturing essential shape characteristics. These calculated Hu moments are then compared to those of known shapes, enabling the classification of the object based on its closest match. In addition to color and shape, the alphanumeric information contained within the object is also of interest. To address this, a well-established technique known as Optical Character Recognition (OCR) is employed. OCR algorithms are designed to recognize and extract alphanumeric characters from images. By applying OCR algorithms to the object's image, the alphanumeric information is identified and extracted, facilitating its classification.

#### Localization

In the context of object localization, the process involves considering three primary input data sources. Firstly, height information is derived from a lidar sensor, providing vertical positional data. Secondly, the camera's orientation, acquired from a gimbal system, furnishes the angular orientation of the camera with respect to the UAV's reference frame. Lastly, the GPS location of the UAV itself is obtained. It is crucial to note that all three input data must be collected simultaneously to ensure accurate object localization. In addition, the Focal Lenght, Image Width and Sensor Wisfth of the camera was known. After getting these informations, we applied Ground Sample Distance method to acquire the possible location of the ROI. 

<p align="center">
  <img src="/images/gsd.png" alt="Figure 2. Ground Sample Distance Method"/>
</p>

<p align="center">
  <em>Figure 2. Ground Sample Distance Method [1] (https://www.researchgate.net/figure/Scheme-of-the-GSD-in-function-of-the-factors-of-flight-height-focal-length-and-geometric_fig5_344125652)</em>
</p>

## Competition and Results

### Preparation

Our participation in the AUVSI SUAS 2022 competition entailed an extensive and fulfilling journey spanning a duration of eight months. As a multidisciplinary team comprising members from Aerospace, Mechanical, Metallurgical, and Materials Engineering disciplines, we collectively embarked on a comprehensive exploration of unmanned aerial vehicle (UAV) design, construction, and operation. Engaging in this endeavor provided me with invaluable experiences that will undoubtedly contribute to my future endeavors.

One of my notable responsibilities involved meticulous planning and task allocation among team members, taking into account their academic commitments and the demands of the competition schedule. This undertaking enabled me to develop essential skills in project management and effective teamwork, while also deepening my understanding of the importance of balancing various academic and extracurricular responsibilities. Despite the challenges imposed by our rigorous academic pursuits, our collaborative efforts proved to be both gratifying and demanding.

The competition itself served as a platform for us to translate theoretical knowledge acquired in our academic pursuits into practical applications. This process pushed the boundaries of our understanding and allowed us to witness firsthand the real-world implications of our academic studies. Through rigorous testing and evaluation of our UAV, I gained invaluable insights and practical experience, greatly augmenting my overall learning experience.

<p align="center">
  <img src="/images/comp.jpg" alt="Figure 3 - Competition Preparing Stage"/>
</p>

<p align="center">
  <em>Figure 3 - Competition Preparing Stage</em>
</p>

### Competition Details

**Location:** The AUVSI SUAS 2022 competition took place from June 15th to 18th at St. Mary's County Regional Airport (2W6) / UMD UAS Test Site.

**Mission Testing:** During the mission testing phase, as a conscientious participant, we encountered several challenges that required attention, notably related to the stability of WiFi connections, which subsequently impacted the overall performance of the system. It is important to acknowledge that these challenges, although inconvenient, provided valuable learning experiences and opportunities for improvement.Despite the aforementioned challenges, the mission testing phase proved to be a valuable endeavor, offering profound insights and opportunities for refinement. In particular, the involvement of former NASA engineers in this phase provided us with invaluable expertise and guidance. Their extensive experience and knowledge contributed to our understanding of best practices, cutting-edge technologies, and problem-solving approaches within the field of mission testing.

**Flight Video:** You can witness our flight video during the competition.

<iframe width="560" height="315" src="https://www.youtube.com/embed/eu7qqW2X3FY" frameborder="0" allowfullscreen></iframe>

### Results

Teams participating in the AUVSI SUAS 2022 competition were evaluated based on Mission Rank, Flight Readiness Review Video Ranking, and Technical Design Paper Ranking, ultimately contributing to their Overall Rank. Here are our team's rankings:

- **Technical Design Paper Rank:** 2
- **Flight Readiness Review Rank:** 7
- **Mission Demonstration Rank:** 12
- **Overall Rank:** 10

You can check the detailed rankings [here](https://docs.google.com/spreadsheets/d/e/2PACX-1vSV0_wulZ_djNrAeuGUOWQXyDoUyD6lgD5H7W9tqT8LZu__uv6s0OiEsDP0lbRetUTWTqQ9S1RAdvAr/pubhtml#). Additionally, our Flight Readiness Review video is available for viewing below.

<iframe width="560" height="315" src="https://www.youtube.com/embed/zmkGAIbsrh4" frameborder="0" allowfullscreen></iframe>
