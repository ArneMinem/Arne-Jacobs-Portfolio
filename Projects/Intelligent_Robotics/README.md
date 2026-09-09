# Behaviour-based vs Evolutionary Robotics
`October 2026 - November 2026`

See our poster [here](IR_Poster_Final_Version.pdf) and our video [here](https://youtu.be/HLEo8Xrrw0U).

## About the module

This project was carried out as part of the Intelligent Robotics module (F20/21RO) at Heriot-Watt University.

## The team

I was part of a team of 4 students from Heriot-Watt University's School of Engineering and Physical Sciences.

We received a grade of 92% for the project!

## The robot

We worked with a simulated e-puck robot (Cyberbotics, 2019), tested across three different environments and behavioural approaches.

## The project

The goal was to compare two fundamentally different ways of designing autonomous robot behaviour: behaviour-based robotics, where the control logic is manually written and tuned, and evolutionary robotics, where a controller emerges from a genetic algorithm rather than being hand-coded. To do this properly, we split the work into three tasks:

* **Task 1 (BBR)**: the robot follows a line while avoiding obstacles.
* **Task 2 (BBR)**: the robot detects and moves towards a light source while avoiding obstacles.
* **Task 3 (ER)**: an evolutionary system based on a genetic algorithm learns to follow a line and complete a full turn while avoiding an obstacle.

## Results

Both behaviour-based tasks worked reliably: the line-following robot tracked the line and avoided every obstacle, and the light-following robot correctly detected the light source and moved towards it without ever hitting a wall or obstacle, though its motion became a bit jumpy near obstacles. The evolutionary system showed clear improvement over generations, with fitness climbing from generation 1 to generation 200 and the best-performing population converging on a smooth, consistent circuit, completing a full loop in around 1:12 to 1:14 seconds.

Comparing the two approaches, we found they share the same underlying constraints (sensor-driven, task-oriented, and both requiring tuning) but differ sharply in philosophy: behaviour-based control is rule-based, interpretable and predictable but scales poorly and needs manual tuning for every new situation, while evolutionary control is emergent and self-optimising but computationally costly, unpredictable and hard to interpret.

## My role in the project

I was responsible for **Task 2**, the light-following behaviour-based controller. Building on the line-following logic from Task 1, I designed and implemented three additional algorithms: light detection, to determine the direction a light source is coming from; turn-to-light, to orient the robot towards it; and move-to-light, to drive the robot in that direction once oriented. I validated the controller in a dedicated light arena, confirming it reliably found and approached the light source while never colliding with obstacles or walls, and identified the residual jumpiness near obstacles as a limitation for future refinement.

I also contributed to the comparative discussion between the behaviour-based and evolutionary approaches, helping frame the trade-offs between manual and evolved design that structured the poster's conclusion.

## Conclusion

This project gave me hands-on experience designing a full behaviour-based control pipeline from sensor reading to motor output, and a much clearer sense of when manual, rule-based control is the right tool versus when an evolved, emergent approach is worth its extra cost and unpredictability. Seeing both paradigms solve related problems side by side, on the same robot, made the trade-offs concrete rather than theoretical.

Development of:

* Knowledge: behaviour-based robotics, evolutionary robotics, genetic algorithms, sensor-driven control
* Skills: Webots/Cyberbotics simulation, controller design, flowchart-based algorithm design, e-puck sensor programming
* Competencies: problem-solving, autonomy, comparative analysis, teamwork