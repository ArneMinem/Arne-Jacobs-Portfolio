# Tiny ROS based car

This project was devided in two parts:
- The first part was to create the car model in Inventor, print some of the parts with a 3D printer and assemble the car.
- The second part was to add the electronic components to the car and program it using ROS2 to move around.

Each step was done in a group of around 5 students.

## First part

For the first part of the project I mainly worked on my own because I love desinging and assembling things but also because my teammates had a lot of other things on their minds. I designed the car in inventor, printed the needed parts and assembled the car.

Since I finished the assembly of the car before the other groups I also helped them with their cars and assembled ours further by adding some extra parts for the second part of the project.

You can find more information of the first part [here](Part1.md).

## Second part

For the second part the groups changed a bit and I arrived in a group with 5 other students, [here](https://github.com/ArneMinem/Mystery_Machine_ROS) you can look at our repository.
Since their car was not completely assembled from the first part I helped them with that and we started to add the electronic components to the car.

Then we split up in 3 groups and together with Simon and Main we checked the functionnality of the differents sensors' drivers.

The following sessions we separated in 2 groups. Matti, Main and I worked on the ROS structure of the car. Therefor we sat together and discussed how we wanted to structure the code and what we wanted to implement. Then we split this into tasks and distributed them between us. We specified which format the messages should have and how the nodes should communicate with each other so that we could work on our tasks independently but still be able to merge them together. I mainly worked on the Kalman Node in which there was also some Lambert93 to GPS conversion involved. I also helped Main with the GPS node and Matti with the control node since I finished my tasks ahead of time.

At the end we arranged a supplementary meeting to test the car and finalize the project together. But there were some issues. Building the project on the computer went well but when we tried to run the project on the car it didn't work. The build never stopped. Another group also tried building their project on the car and encountered the same problem. Thus, we think that the projects might have been too heavy for the car to handle. We did not have the time to try solving the issue by using Docker but this might have been a solution.

## Conclusion

I really enjoyed working on this project. I learned a lot about ROS2 and how to structure a project in a way that it is easy to work on it in a group. I also learned a lot about the Kalman filter and how to use it in a project. I would have liked to have more time to test the car and to try to solve the issue with the build on the car. But I am still happy with the result and I am proud of what we achieved in the time we had. I would love to work on a similar project in the future.

## Skills learned

- ROS2
- Kalman filter
- Lambert93
- Group work
- Structuring a project
- 3D printing
- Assembly
- 3D printing
- Inventor
- Python
- C++
- Git
- Docker
- Raspberry Pi
- Electronics


