---
title: "AUVSI SUAS 2022 Competition"
excerpt: "AUVSI SUAS is an annual competition that challenges student teams to design, build, and operate unmanned aerial vehicles (UAVs or drones). The competition typically involves a series of missions that test the capabilities of the teams' autonomous systems. These missions often include tasks such as autonomous flight, target identification, and payload delivery.<br/><img src='/images/kesekci_4.png' width='600' height='450'>"
collection: portfolio
---

## Competition Tasks

You can get more information about the competition from [this link](https://suas-competition.org/competitions).

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

I was a coordinator of the Software and Electronics Subteam. I My primary software responsibility was to develop an obstacle avoidance algorithm for the Obstacle Avoidance mission. Additionally, each member of the subteam was responsible for the electronic integration of our UAV (Kesekci). We also conducted the necessary research for avionics, and I specifically took charge of the GPS module selection.

### Object Detection 

In the second mission of the competition, navigating through an environment with cylindrical obstacles was the primary objective. To successfully complete this task, suitable routes for the UAV needed to be determined. We explored various route planning algorithms, including Rapidly Exploring Random Trees (RRT) and A*.

#### RRT Algorithm

RRT is a widely used method in route planning. Introduced by Steven M. LaValle and James J. Kuffner Jr., this algorithm creates a tree of iteratively randomly selected points in the robot's reference coordinate system. The process involves extending the tree by selecting a random point, moving the robot from the nearest node to the random point while avoiding collisions, and creating a new node in the tree. Due to its capacity for dynamic obstacle avoidance and excellent performance in environments requiring complex route planning, RRT has found applications in various sectors, such as planning the movements of robotic arms and directing autonomous vehicles. However, considering the competition's requirements of few and only cylindrical obstacles, we deemed the computational load of this algorithm excessive for the second mission.

<p align="center">
  <img src="/images/rrt_2.png" alt="Figure 1 - RRT Algortihm"/>
</p>

<p align="center">
  <em>Figure 1 - RRT Algortihm[1](https://www.researchgate.net/publication/366866319_An_Integrated_RRTSMART-A_Algorithm_for_solving_the_Global_Path_Planning_Problem_in_a_Static_Environment)</em>
</p>


#### A* Algorithm

A* is an algorithm that determines the route with the lowest cumulative cost. The cost is determined based on various parameters for paths between each node. For this competition, the sole cost parameter was set as distance. The algorithm calculates the cost from the starting node to the current node, the cost from the current node to the target node, and, for each node associated with the current node, the algorithm selects the node with the lowest cost. This process is repeated until the target node is reached, and the path with the lowest cost is found. While the A* algorithm's main advantage is its optimality, considering the competition requirements, it was thought that using this algorithm would impose an excessive computational burden.

<p align="center">
  <img src="/images/a.png" alt="Figure 2 - A* Algortihm"/>
</p>

<p align="center">
  <em>Figure 2 - A* Algortihm</em>
</p>

#### Team-Developed Custom Algorithm

Recognizing the complexity and additional computational load of the mentioned algorithms for the competition, our team decided to develop a custom algorithm. At its core, the algorithm focused on navigation between specific waypoints.

The algorithm initially disregards obstacles and determines suitable waypoints between the start and target locations. Subsequently, if there is an obstacle or proximity to an obstacle along the route between two waypoints, the algorithm finds a more suitable and safer third waypoint. Geometric operations are used to find this third waypoint, based on the intersection scenarios of a line and a circle. If there is no intersection, the algorithm checks whether there is a safe distance between the route and the obstacle. If there is no safe distance, a third waypoint away from the obstacle is found based on the user-defined safe distance parameter. The same process is applied if the route is tangential or intersecting the obstacle. This process is summarized in Figure 3. The user can flexibly define the safe distance parameter, providing adaptability to the algorithm's use based on the robot's characteristics and obstacle types. Finally, equations 1 and 2 provide the coordinates calculation of the safe third waypoint.

<p align="center">
  <img src="/images/obstacle.png" alt="Figure 4"/>
</p>

<p align="center">
  <em>Figure 3</em>
</p>

$x = \frac{x_1 + x_2}{2} + [(K + M) \times \sin(\alpha)] \quad$ (1)

$y = \frac{y_1 + y_2}{2} + [(K + M) \times \cos(\alpha)] \quad$ (2)


This process is applied to all waypoints, yielding a sequence of waypoints that do not intersect with obstacles. In this way, the safest and shortest route is determined. The application of this algorithm to specific waypoints can be observed in Figure 4.

<p align="center">
  <img src="/images/obstalce_avoidance.png" alt="Figure 4"/>
</p>

<p align="center">
  <em>Figure 4</em>
</p>

## Competition and Results

### Preparation

Our journey towards the AUVSI SUAS 2022 competition was an intensive and rewarding experience that spanned eight months. Collaborating across disciplines—Aerospace, Mechanical, Metallurgical, and Materials Engineering—my team and I delved into the intricacies of designing, building, and operating unmanned aerial vehicles (UAVs). Despite the challenges posed by our demanding academic schedules, the collaboration proved to be a joyous yet demanding endeavor. The competition provided a platform for us to translate theoretical knowledge into practical applications, pushing the boundaries of our understanding. Through rigorous testing of our UAV, I gained valuable insights and practical experience that enhanced my learning.

### Competition Details

**Location:** The AUVSI SUAS 2022 competition took place from June 15th to 18th at St. Mary's County Regional Airport (2W6) / UMD UAS Test Site.

**Mission Testing:** As a responsible member during the mission testing phase, we encountered some challenges, particularly with wifi connections, which affected the overall performance. However, despite these hurdles, the mission test provided valuable insights and opportunities for improvement.

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
