---
title: "2023 Teknofest Mixed Swarm Competition"
excerpt: "In 2023, I actively participated in the Swarm UAV Competition organized as part of the TEKNOFEST Technology competitions. Tasked with developing software and algorithms for Unmanned Aerial Vehicles (UAVs) operating collaboratively as a swarm, the competition aimed to assess the practical functionality of these algorithms in real-world conditions. As a member of my team, our objective was to comprehend the operational aspects of software algorithms for swarming UAVs and explore their potential applications in both civilian and military domains.<br/><img src='/images/swarm-drones.jpg' width='600' height='450'>"
collection: portfolio
---

## About the Competition

The Swarm UAV Competition, organized within the TEKNOFEST Technology competitions, focuses on Swarm Unmanned Aerial Vehicles (Swarm UAV), a technology gaining increasing importance in both civilian and military applications. The competition's primary goal is to develop software and algorithms for UAVs capable of fulfilling specified missions as a swarm. The competition showcases the practical functionality of these algorithms by deploying Swarm UAVs in real-world conditions. Key objectives include understanding how software algorithms for swarming UAVs operate, exploring the technology's potential in civil and military applications, and encouraging young talents in this field. Given the transformative potential of Swarm UAVs in daily life and defense strategies, the competition aims to contribute to the technology's development.

## My Responsibilities

My responsibilities included working on controllers (Mellinger, PID, etc.) and designing software algorithms for navigation and trajectory. Also I was responsiblo to manage the project progression as team captain.

## 1.Position Controller

The position controller was designed to enable agents to move from one point to another. Due to the restrictions on using the goTo functions of Crazyswarm and Cflib libraries specified in the competition rules, a custom module was required. Several conditions were considered in developing this module:

1. Taking into account the aerodynamics and mechanics of Crazyflie 2.x drones used in the competition.
2. Considering the limitations of the embedded controllers in Crazyflie drones, determining how well they can follow the sent commands.
3. Achieving the target location with minimal margin of error.
4. Ensuring stability during movement while minimizing time sacrifice.

### Static Algorithms

The first set of algorithms was based on the relationship between path, speed, and time, generating straight paths. Parameters from Table 1 were used for route creation, followed by deriving the required velocity vectors using Equation 1.

*Table-1. Required Parameters for Static Algorithm*

| Parameter      | Description        |
| -------------- | ------------------ |
| Start Point    | (X<sub>1</sub>, Y<sub>1</sub>, Z<sub>1</sub>) |
| End Point      | (X<sub>2</sub>, Y<sub>2</sub>, Z<sub>2</sub>) |
| Time           | t                  |
| Deceleration   | a                  |

$x(t) = x_0 + vt + \frac{1}{2}at^2$ (1)

Python was employed to implement the algorithm, and it was tested in simulation for a single agent. The results indicated stable operation with a low margin of error, especially when limiting speed and acceleration values. However, concerns arose regarding the adaptability of this algorithm to real-world scenarios involving multiple agents, where unforeseen changes during flight could occur. Due to the inability to respond to unpredictable changes, such as interactions between agents, communication disruptions, and errors in individual controllers, it was decided that this algorithm was not suitable for use.

### Feedback Algorithms (Controllers)

Given the limitations of static algorithms for dynamic systems, feedback control systems, especially PID (Proportional-Integral-Derivative) controllers, were considered. PID controllers are widely used in various applications due to their simplicity, robustness, and effectiveness in regulating system performance. The decision was made to develop a PID controller.

The first step in developing a controller is accurately defining the system. Research was conducted to understand the commands that could be sent to the Crazyflie drone using Cflib. Commands such as position_setpoint(x, y, z, yaw), full_setpoint(roll, pitch, yawrate, thrust), and send_velocity_world_setpoint(vx, vy, vz, yaw) were identified. Using velocity commands for effective control, a system was designed as depicted in Figure 1.

<p align="center">
  <img src="/images/pid_position.png" alt="Figure 1 - Position Controller"/>
</p>

<p align="center">
  <em>Figure 1 - Position Controller</em>
</p>



After designing the system, a PID controller was implemented in Python. Subsequent tests were conducted in the simulation, and PID parameters were calibrated. Finally, real-world tests on a Crazyflie confirmed that the controller operated optimally under various conditions.

To showcase the performance of developed position controller, I have prepared two videos. The first video presents simulation results using Gazebo with CrazyS, offering insights into the algorithms' behavior in a controlled virtual environment. The second video showcases real-life tests conducted with a Crazyflie 2.1 equipped with the Lighthouse positioning system, demonstrating the practical implementation of our algorithms in a physical setting.

<iframe width="560" height="315" src="https://www.youtube.com/embed/SUDe9ivEPgo" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/U0jJdcwHOl4" frameborder="0" allowfullscreen></iframe>

## 2.Trajecteroy Generation and Mellinger Controller

### Smooth Trajectory Planning

In the competition, the requirement is to navigate smoothly through obstacles. Planning a route solely based on waypoints wouldn't meet this criterion. Therefore, a literature review was conducted on how to achieve smooth trajectory tracking using intermediate waypoints. The work done here is based on the research of [Kumar and Mellinger(2011)](https://ieeexplore.ieee.org/abstract/document/5980409).

#### Mellinger Controller

The Mellinger controller utilizes a non-linear model of the dynamics of a quadcopter, employing a feedback loop to accurately track the desired position and orientation of the drone. The feedback loop consists of an attitude controller and a position controller. The attitude controller manages the orientation of the drone, while the position controller governs translational motion. The attitude controller employs a non-linear controller using the rotation matrix and quaternion representation of the drone's attitude. Additionally, the position controller compares the desired and current positions using data from sensors, producing thrust commands to control the drone's position with a proportional-derivative (PD) controller. The attitude controller, in turn, generates torque commands by comparing the desired and current attitudes using data from the position controller and sensors.

The Mellinger controller has been implemented for the Crazyflie 2.X drones intended for use in the competition. Therefore, it is concluded that this controller can be readily employed if the necessary trajectory can be generated.

#### Trajectory Generation

To ensure smooth navigation to the destination, trajectory planning is essential. Numerous trajectory generation algorithms exist for quadcopters, and this stage is critical for four-motor drone control.

Piecewise polynomial functions are significant methods used in trajectory calculations. By solving a group of linear equations obtained from drone dynamics and boundary conditions, the coefficients of the polynomial function can be determined. The trajectory obtained for an environment including cylindirical obstacles is given in Figure 2.

<p align="center">
  <img src="/images/pid_position.png" alt="Figure 1 - Position Controller"/>
</p>

<p align="center">
  <em>Figure 2 - Example Trajectory</em>
</p>

Taking derivatives of this trajectory provides the necessary position, velocity, and acceleration vectors. Through experiments, it has been observed that sending only the position vector to the agents at the required frequency enables successful trajectory tracking. The following video shows the applied alforithms for trajectory tracking with a Crazyflie 2.1 and Lighthouse Positioning System.

<iframe width="560" height="315" src="https://www.youtube.com/embed/oY1j8kOTbE8" frameborder="0" allowfullscreen></iframe>

## Important Reminder

Since this was a team project, I cannot share codes without permission of my team 😞.