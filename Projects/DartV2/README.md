# Car through Labyrinth

[Here](https://github.com/ArneMinem/DARTv2) is the repository for this project.

## Description

The goal of this project was to program a DartV2 robot to navigate through a labyrinth. Equipped with a camera, an encoder, a gyroscope, and distance sensors, the robot was designed to detect lines on the ground, measure distance traveled, determine orientation, and detect walls within the labyrinth.

However, the camera was not utilized in this project due to the absence of lines on the ground.

The robot was programmed to follow the walls of the labyrinth and complete the entire tour without making contact with any walls. The project could be completed individually or in pairs.

## My Work

I worked alone on this project.

The first step involved simulating the robot in CoppeliaSim to test the algorithm. A virtual model of the robot and the labyrinth was provided for this purpose.

Next, I programmed the robot in Python using virtual encoders, a virtual gyroscope, and virtual distance sensors. The algorithm instructed the robot to follow the walls of the labyrinth until it reached a certain distance from a wall in front of it. It would then detect the side without a wall and turn in that direction. The robot would continue moving until it detected another wall in front of it, repeating the process. To achieve wall following behavior, a PID controller was implemented to control the robot's speed and distance from the walls. If the robot approached a wall too closely, it would turn in the opposite direction to maintain a safe distance.

Once the simulation was successful, I proceeded to program the real robot. This required adapting the code to work with the actual sensors and motors of the robot. Due to differences between the simulation and the real robot, such as sensor uncertainties, I had to fine-tune the PID controller and the robot's speed to ensure proper functionality.

Although the robot nearly completed the entire labyrinth without touching the walls, it started to lose its trajectory towards the end.

I have recorded two test videos: [test1](https://youtu.be/eEG9c8C--tY) and [test2](https://youtu.be/_L4Z3qVxiXU).

In both cases, the robot encountered issues at the same location. The first time, the problem was caused by the robot getting too close to the wall. I managed to improve the code by reducing the sensor refresh rate, resulting in a more stable robot. However, this led to the robot frequently spinning in place before moving forward. This is also why, in the second video, everything went well until the robot started spinning and detected the absence of a diagonal wall, causing it to collide with the wall.

Unfortunately, I did not have enough time to address this issue. Nonetheless, my robot performed admirably compared to my peers, and I am satisfied with the results.

## What I Learned

Through this project, I gained experience in using a PID controller to control a robot's speed and distance from walls. I also learned how to utilize the robot's sensors to enable wall following behavior in a labyrinth. Additionally, I acquired knowledge in tuning the PID controller for real-world applications.

Furthermore, I expanded my proficiency in Python, CoppeliaSim, and working with the DartV2 robot. I also learned how to implement state machines for robot programming.

