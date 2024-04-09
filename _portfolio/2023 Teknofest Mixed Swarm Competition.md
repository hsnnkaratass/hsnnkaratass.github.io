---
title: "2023 Teknofest Mixed Swarm Competition"
excerpt: "The primary focus of this competition revolved around the comprehensive development of software and algorithms tailored specifically for Unmanned Aerial Vehicles (UAVs) operating collaboratively in a swarm configuration. By simulating real-world conditions, the competition sought to assess the practical functionality and efficacy of these algorithms in dynamic operational scenarios. As an integral member of my team, our collective objective was to gain a profound understanding of the operational intricacies associated with software algorithms for swarming UAVs. This entailed exploring and analyzing their potential applications across diverse domains, encompassing both civilian and military sectors. By delving into the multifaceted aspects of swarm behavior and coordination, we aimed to unlock the vast potential of these collaborative UAV systems..<br/><img src='/images/swarm-drones.jpg' width='600' height='450'>"
collection: portfolio
---

## About the Competition

The Swarm UAV Competition, organized within the TEKNOFEST Technology competitions, focuses on Swarm Unmanned Aerial Vehicles (Swarm UAV), a technology gaining increasing importance in both civilian and military applications. The competition's primary goal is to develop software and algorithms for UAVs capable of fulfilling specified missions as a swarm. The competition showcases the practical functionality of these algorithms by deploying Swarm UAVs in real-world conditions. Key objectives include understanding how software algorithms for swarming UAVs operate, exploring the technology's potential in civil and military applications, and encouraging young talents in this field. Given the transformative potential of Swarm UAVs in daily life and defense strategies, the competition aims to contribute to the technology's development.

You can get the detailed information about competition and mission from [this link](https://www.teknofest.org/en/competitions/swarm-uav-competition/)

## My Responsibilities

My responsibilities included working on collision avoidance of the swarm members. Also, I worked with cflib library to communicate with the Crazyflie quadcopter.

## Collision Avoidance

In order not to have collision between swarm members while navigating as a swarm and independently, there should be some control for the paths of the swarm members. After conducting a comprehensive review of the relevant literature, we decided to employ the method of "Hybrid Mutual Velocity Obstacles" as the collision avoidance module, as discussed in the article by Snape et al [[1]] (https://ieeexplore.ieee.org/document/5746538). According to this method, each member of the swarm perceives the movements of its surrounding entities and makes decisions regarding its own motion accordingly. Within the determined safe distance, it monitors the trajectories of its own velocity vector and the velocity vectors of other swarm members to ensure the absence of any collisions. Furthermore, this method is reciprocal, taking into account that other agents also perceive their surroundings and adjust their trajectories accordingly, thereby mitigating oscillations.

The operation of the method can be summarized as follows:

1- For the module to function when the distance between agents falls below the safe threshold, the first step is to determine the safe distance.

2- If another agent enters the safe zone of an agent, the possibility of a collision is checked.

3- If a collision is detected, a velocity obstacle is determined for the leading agent. The velocity obstacle is a virtual cone volume that determines the directions of velocity vectors for which a collision would occur with other agents, as illustrated in Figure 1. A virtual circle with a radius equal to the sum of the radii of two agents is established. Tangents are drawn from the selected agent's center to the circle, defining the velocity obstacle cone.

<p align="center">
  <img src="/images/fig1.png" alt="Figure 1 - Velocity Obstacle Area"/>
</p>

<p align="center">
  <em>Figure 1 - Velocity Obstacle Area</em>
</p>


4- The agent should select a new velocity vector that is closest to the desired destination but remains within the determined velocity obstacle. The article discusses three different methods for performing this task. In our particular case, it is deemed sufficient to utilize the first method, which involves determining the velocity obstacle cone. This choice is justified by the fact that, in our project, the agents will not approach each other and the number of agents is relatively small.

<p align="center">
  <img src="/images/fig2.png" alt="Figure 2 - Collision Free Vector"/>
</p>

<p align="center">
  <em>Figure 2 - Collision Free Vector</em>
</p>

5-These procedures are repeated for other agents that are within the safe distance and at risk of collision. By applying the same methodology, a new velocity vector is determined for each of these agents, ensuring collision-free trajectories.

The rationale behind the second and third methods, as indicated in the article, can be elucidated as follows. Considering that the velocity obstacle determination process is applied to both agents involved, the responsibility of collision avoidance is shared by both agents. Consequently, the velocity vectors of the agents are updated by subtracting twice the magnitude of the previous velocity vector from the newly determined velocity vector, as illustrated in Figure 2. This approach ensures that both agents contribute to the avoidance of collisions.

<p align="center">
  <img src="/images/met2.png" alt="Figure 3 - Reciprocal Collision Free Vectors"/>
</p>

<p align="center">
  <em>Figure 3 - Reciprocal Collision Free Vectors</em>
</p>


The developed system has been validated through simulations and real-life tests, providing evidence of its functionality. Simulation images are depicted in Figure 4, showcasing the results. The conducted tests were designed with consideration for a competitive environment. As mentioned earlier, in scenarios involving obstructed navigation, there is a possibility of collision between agents. Specifically, when two agents are moving in similar directions rather than directly towards each other, collision scenarios can arise. To account for all possibilities, the situation where agents converge at the same point was also tested, and no collision occurred. In Figure 4.a, the straight red and green lines represent the initial directions of the agents, while the red lines generated from behind the left agent illustrate the planned trajectories to prevent collision.

<p align="center">
  <img src="/images/cfp.png" alt="Figure 4 - Collision Free Paths"/>
</p>

<p align="center">
  <em>Figure 4 - Collision Free Paths</em>
</p>


Below you can watch the test flight of the first mission. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/oQFZXaJ2mFo?si=yc1SWivwSDk1gkk_" frameborder="0" allowfullscreen></iframe>

## Important Reminder

Since this was a team project, I cannot share codes without permission of my team 😞.