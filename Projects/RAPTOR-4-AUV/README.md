# RAPTOR-4-AUV: Generalized 6-DOF Underwater Control via GPU-Parallel Meta-Imitation Learning
`3rd of June 2026 - 18th of August 2026`

See the full MSc Dissertation project report [here](ArneJacobs_H00508832_DrCarluchoIgnacio.pdf) and the presentation slides [here](260810_MSc_Presentation_Arne_JACOBS_H00508832.pdf).

## About the project

This project served as my MSc Dissertation in Robotics at Heriot-Watt University. The core problem addressed was that autonomous underwater vehicle (AUV) controllers typically require manual retuning whenever variations in hull, payload, or ballast occur. Adapting recent advancements in aerial robotics, this research investigated whether a single recurrent policy could control a diverse bank of 6-degree-of-freedom underwater vehicles across a 30-fold mass range (5–150 kg) without any per-vehicle retuning.


## The methodology

To achieve population-scale training, I leveraged GPU-parallel physics simulation to invert the usual sample-efficiency trade-offs.

* I trained 1,000 independent Proximal Policy Optimisation (PPO) "teacher" policies, each specialized for a distinct, statically configured AUV hardware setup in MuJoCo-XLA.


* These specialists were then distilled into a single gated-recurrent-unit (GRU) "student" policy using DAgger-style meta-imitation learning.


* I constructed a matched domain-randomisation baseline which was trained by actively randomising parameters like buoyancy across its training episodes (unlike the static-environment teachers), to act as a strict control condition for evaluating the neural architecture.


* Sim-to-sim transfer was validated by bridging the trained policy to a physically distinct BlueROV2-Heavy model in Stonefish, an independent CPU-based marine-robotics engine.



## Key findings and results

The recurrent student matched the per-vehicle specialists on nominal physics and drastically outperformed them under off-nominal stressors.

* Under strong buoyancy conditions, the generalist student reduced position error from 19.2 cm to 3.5 cm compared to the specialist.


* By running a linear probe on the student's hidden state, I recovered the buoyancy parameter for 300 held-out vehicles at $R^2 = 0.87$, proving the network was actively performing implicit system identification rather than just reacting to errors.


* I discovered a critical training condition: vehicle-identity parameters like buoyancy must be held fixed per teacher during distillation; re-randomising them as nuisance noise silently corrupts the training labels and causes a performance plateau.


* Surprisingly, the much cheaper single-policy domain-randomisation baseline (exposed to continuous buoyancy variations during its training loop) matched or exceeded the student on single-axis variations. This proved that recurrence primarily buys the composition of several identity axes rather than superior single-axis adaptation.


* The baseline also degraded more gracefully outside the training distribution, maintaining a 100% success rate where the distilled student fell to 53–71% at the light-mass boundary.



## Demonstration Videos and Evaluations

The following clips and full-schedule evaluations demonstrate the key qualitative behaviors, sim-to-sim transfers, and stress tests referenced in the study:

### Core Comparison Clips

* **V1: Specialist vs. Distilled Student** — Both policies evaluated on the same body while buoyancy is swept from 0.35 to 1.78 ([Watch V1](https://youtu.be/UGJmcUIegGg)).


* **V2: Hardware Swap with Hidden State Preserved** — Mid-flight vehicle exchange to a much heavier body without resetting the recurrent state ([Watch V2](https://youtu.be/iNicQTPlfDs)).


* **V3: Buoyancy Driven to Controllability Limit** — Buoyancy swept outward until the analytic bound of Equation 6 is reached and hold collapses ([Watch V3](https://youtu.be/0z2d5RWMgxU)).


* **V4: Mid-Flight Payload, Zero-Shot** — Unseen payload added during hover; specialist sinks while student compensates ([Watch V4](https://youtu.be/TblOceWNGrY)).


* **V5: Sim-to-Sim Transfer (BlueROV2 in Stonefish)** — Delay-free vs. delay-trained students driven through identical trajectories in an independent engine ([Watch V5](https://youtu.be/btPi0lSPvYA)).


* **V6: Thruster-Fault Sweep** — Station-keeping under a severe asymmetric actuator fault out-of-distribution ([Watch V6](https://youtu.be/dMx9MxsK5fM)).


* **V7: Randomisation Baseline vs. Student** — RQ4 control condition compared against the distilled student under a buoyancy sweep ([Watch V7](https://youtu.be/AzwFrnhTi2Q)).


### Extended Evaluations & Full Schedules

* **E1: The 17-Phase Scenario, End-to-End** — The full 102-second stress schedule executed in lock-step, including moving-target phases ([Watch E1](https://youtu.be/DIOe1ay6aWY)).


* **E2: Stonefish Dual, Tilt Schedule** — Two BlueROV2s driven simultaneously through large-attitude schedules from level hold to 160° inversion ([Watch E2](https://youtu.be/g-vFBkhs4zE)).


* **E3: Randomisation Baseline vs. Student (Interactive)** — Live interactive variation of target pose, buoyancy, payload, and disturbance with full telemetry ([Watch E3](https://youtu.be/EVKFf9hQa78)).


* **E4: The Randomisation Baseline in Stonefish** — Qualitative observation of the baseline transferred to the independent engine ([Watch E4](https://youtu.be/4RkMvup5_Fg)).


* **E5: The Student in Stonefish (Driven by Hand)** — Free-form interactive pose commands issued to the distilled student post-message-timing correction ([Watch E5](https://youtu.be/CkhysE8fdVM)).


## Technologies and skills

* **Knowledge:** Deep reinforcement learning, 6-DOF AUV dynamics, teacher-student distillation, sim-to-sim transfer, implicit system identification.


* **Tools:** Python, JAX, MuJoCo-XLA, Flax, Optax, ROS2, Stonefish, GRU, PPO.