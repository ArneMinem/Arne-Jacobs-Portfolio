# Autonomous Chess-Playing Robot
`B51RO Case Study (Mechanical Robotic Systems at Heriot-Watt University)`
`15th of January 2026 - 28th of March 2026`

Repurposing a Creality Ender 3 Pro 3D printer into a fully autonomous chess-playing robot, using computer vision, a chess AI engine, and electromagnetic pick-and-place. The project was built for **£0** out of a £245 market-value budget.

## Project materials

The full write-up and slide deck for this project are also available in my portfolio:

* [Full case study report](3_CaseStudyreport.pdf)
* [Presentation slides](B51RO_Group_3_ChessRobot.pdf)
* [Video demonstration](img/Demo_Video.mp4)

---

## About the case study

The B51RO case study challenges student groups at Heriot-Watt University's School of Engineering and Physical Sciences to design, build, and demonstrate a working robotic system from scratch, within a limited budget and using components sourced from campus labs. Our group chose to repurpose a 3D printer's Cartesian motion system into a robot capable of playing a full game of chess autonomously against a human opponent.

## The team

We were a team of 5 students. In practice, I did the large majority of the hands-on technical work (the mechanical build, vision pipeline, kinematics, and system integration) while the other members contributed through research, coordination, and specific deliverables such as the literature review and the chess-piece CAD files. The project was presented as a collective effort in line with the module's teamwork assessment criteria, but I'm the one who can speak in depth to the technical implementation below.

## Why chess?

Chess demands precise X-Y-Z Cartesian motion, real-time decision-making, and a full vision-to-motion pipeline. This makes it an ideal, self-contained testbed for integrated robotics: perception, planning, and actuation all in one project.

## Design constraints

* **Fully autonomous**: zero human intervention during gameplay after the opponent's first move.
* **Vision-based**: the system must detect board-state changes from a camera after every human move.
* **Budget-limited**: £50 total budget, with hardware components sourced from campus labs.
* **Safe operation**: low-speed, office-safe motion at all times.

## The robot

We converted a **Creality Ender 3 Pro** by removing its hot-end and replacing it with a custom PETG/PLA-printed toolhead mounting an **RS PRO 150N, 24V DC electromagnet**. The printer's X and Y axes move the electromagnet over an 8×8 grid of chess squares, while the Z-axis is used purely to raise and lower the magnet for pick-and-place operations. Custom 3D-printed chess pieces were designed with a ferrous cap and a geometry optimised for consistent electromagnet engagement and centre-of-gravity stability, so they can be reliably lifted and slid across the board.

## Technical implementation

### Kinematics

Because the Ender 3 Pro is a Cartesian robot with three independent prismatic joints, the Jacobian is simply the 3×3 identity matrix: the inverse kinematics reduces to a direct, closed-form, singularity-free assignment rather than an iterative solve.

```
q1 = X = 26 + (file - 1) × 27 mm
q2 = Y = 38 + (rank - 1) × 27 mm
q3 = Z ∈ {18 mm (pick), 40 mm (transit)}
```

The real engineering challenge wasn't the inverse kinematics but the coordinate transform chain from camera pixels to printer coordinates via homography, which was the actual bottleneck of the project.

### Computer vision

* **Capture:** a Microsoft LifeCam HD-3000 (720p/30fps) mounted on an overhead bracket looks straight down at the board.
* **Perspective correction:** an OpenCV homography rectifies the angled camera view into a top-down 8×8 grid.
* **Grid segmentation:** the rectified image is split into 64 equal-area regions using a calibration JSON generated at startup.
* **Move detection:** frame differencing identifies which square was vacated and which square became newly occupied, translating the human's physical move into board notation.

### Motion control & chess engine

* **Sunfish**, a compact Python chess engine using minimax search with alpha-beta pruning, computes the robot's response. The full game history is passed to it on every call, and it returns the best move in algebraic notation.
* **OctoPrint's REST API** streams G-code to the printer over HTTP, decoupling the chess logic entirely from the printer firmware. Feed rates were kept conservative to prevent piece displacement from inertia during moves.
* **Captured piece handling:** captured pieces are relocated to an off-board holding area *before* the capturing piece is moved into place, avoiding any physical collision on the board.

The overall control loop: connect to the printer → home and park → initialise the move detector and load the calibration grid → watch for a human move over a rolling window of frames → validate legality → handle any capture → execute the move → check for game-over → repeat.

### Bill of materials

| Component | Specification | Market value | Actual cost |
|---|---|---|---|
| Creality Ender 3 Pro | 220×220×250 mm Cartesian printer | ~£180 | £0 (GRID Lab) |
| RS PRO Electromagnet | 150N, 24V DC, 25 mm dia., IP20 | ~£25 | £0 (JN Mechanical Workshop) |
| Microsoft LifeCam HD | 720p/30fps overhead USB camera | ~£30 | £0 (donated by lab) |
| M3/M4 screw kit | Assorted hex bolts & washers | ~£8 | £0 (lab stock) |
| PLA filament (×2 colours) | 1.75 mm, ~125 g used | ~£2 | £0 (lab printer stock) |
| **Total** | | **£245** | **£0** |

## Results

* Full end-to-end autonomous gameplay demonstrated, with zero manual input once the opponent's move was made.
* **Move detection success:** ~80%
* **Pick-up success:** ~95%
* **Average move cycle time:** ~15 seconds, at deliberately low, constrained speeds for safety.

## My role in the project

As Systems Architect & Integration Lead, I drove the project end to end. Beyond the high-level design and hardware procurement, I personally built and debugged the core technical pipeline: the mechanical conversion of the printer (toolhead swap, electromagnet mounting), the closed-form kinematics and homography-based coordinate calibration, the OpenCV move-detection pipeline, the integration of the Sunfish chess engine into a live control loop, and the OctoPrint/G-code interface tying it all together. Getting the vision-based move detection to work reliably under real lighting conditions was the single hardest problem in the project, and solving it, along with wiring every subsystem into one working autonomous loop, was almost entirely my work.

## Conclusion

We successfully converted a Creality Ender 3 into a fully autonomous chess-playing robot, integrating computer vision, AI move generation, and electromagnetic actuation for a total spend of £0. The project reinforced how much of an "easy" kinematics problem can be dwarfed in practice by a "hard" perception problem: a Cartesian robot's inverse kinematics is trivial, but reliably mapping a webcam pixel to a real-world millimetre coordinate under variable lighting is not. Hard-coding the grid calibration rather than relying on live detection each time proved to be the most robust way to sidestep lighting variation, and the printer's naturally slow lead-screw motion turned out to be a safety feature rather than a limitation. It gives plenty of margin against crushing incidents. Overall, the £0 spend also validated our design-for-manufacture-and-assembly and resource-reuse approach.

We received a grade of 82.5% for the project!

## Future work

* **Dynamic difficulty:** currently Sunfish always plays its best move; adding Elo-rated engine levels would let opponents choose a difficulty.
* **On-board display:** use the printer's existing LCD to show game information and handle settings.
* **Voice announcements:** microphone integration for spoken move announcements, which could help visually impaired players use a physical board, or let two players compete purely by voice.
* **Better piece handling:** store captured pieces on the side with automatic repositioning, support saving/resuming a game, and offer chess puzzles.

## Skills developed

* **Knowledge:** Cartesian robot kinematics, computer vision homography and calibration, chess-engine integration, electromagnetic actuation, firmware abstraction via OctoPrint.
* **Skills:** Python, OpenCV, G-code, REST API integration, 3D printing / CAD, low-budget hardware repurposing.
* **Competencies:** systems integration, teamwork, problem-solving under budget constraints, adaptability, project scheduling.