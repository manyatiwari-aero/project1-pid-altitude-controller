# project1_PID_altitude_controller
PID altitude controller simulation for quadcopter — MATLAB Control System Toolbox

# Project 1 — PID Altitude Controller
**Status: Complete**  
**Tool: MATLAB Control System Toolbox**  
**Author: Manya Tiwari | Aerospace Engineering Year 2 | KIIT University**

## What this project does
Simulates a PID controller that holds a quadcopter at a 
target altitude. Models the drone's altitude dynamics as 
a double integrator (1/s²) and designs a PID controller 
to stabilise it using MATLAB's Control System Toolbox.

## The problem
An uncontrolled drone with constant thrust accelerates 
forever — altitude goes to infinity. A controller is 
needed that constantly reads the altitude error and 
adjusts thrust to maintain the target altitude.

## How the controller works
- **P term (Kp):** Pushes based on current altitude error — big gap = big push
- **I term (Ki):** Eliminates the small remaining gap P leaves behind
- **D term (Kd):** Damps oscillations as drone approaches target — acts like a shock absorber

## Development progression

### Step 1 — Uncontrolled drone
No controller. Constant thrust causes altitude to grow 
to infinity. This is the problem being solved.

![uncontrolled drone](droneplant.fig)

### Step 2 — P controller only
Adding proportional control stops infinite growth but 
causes sustained oscillation — drone bounces around 
target forever without settling.

![p controller](pcontroller.fig)

### Step 3 — P + D controller
Adding derivative term damps the oscillations. 
Drone begins to settle but steady state error remains.

![pd controller](p+dcontroller.fig)

### Step 4 — Full PID controller (best result)
Adding integral term eliminates steady state error. 
Drone rises and settles exactly at target altitude.

![full pid](BLOCK_4_PID(5,1,6).fig)

## Results — gain tuning comparison

| Kp | Ki | Kd | Rise Time | Settling Time | Overshoot |
|----|----|----|-----------|---------------|-----------|
| 5  | 1  | 3  | 0.38 s    | 3.34 s        | 24.9%     |
| 8  | 2  | 4  | 0.30 s    | 1.78 s        | 23.4%     |
| **5**  | **1**  | **6**  | **0.28 s**    | **2.85 s**        | **10.0%**     |
| 3  | 0.5| 5  | 0.34 s    | 3.75 s        | 9.0%      |

**Best result: Kp=5, Ki=1, Kd=6**  
Lowest overshoot (10%) with fastest rise time (0.28s).  
Higher Kd provides better damping without sacrificing speed.

## Key observations
- P-only control always oscillates on a double integrator plant
- Increasing Kd reduces overshoot significantly (24.9% → 10.0%)
- Increasing Ki too high causes instability — kept at 1
- Rise time under 0.4s across all combinations — fast response

## Skills used
MATLAB · Control System Toolbox · Transfer Functions ·  
PID Tuning · Step Response Analysis · stepinfo() · Feedback Control

## Files
- `pid_exploration.m` — complete simulation with all 4 blocks
- `simplesystem.fig` — Block 1 stable test system
- `droneplant.fig` — Block 2 uncontrolled drone
- `pcontroller.fig` — Block 3 P-only controller
- `p+dcontroller.fig` — P+D controller
- `BLOCK_4_PID.fig` — Full PID Kp=5 Ki=1 Kd=3
- `BLOCK_4_PID(8,2,4).fig` — Full PID Kp=8 Ki=2 Kd=4
- `BLOCK_4_PID(5,1,6).fig` — Full PID Kp=5 Ki=1 Kd=6 (best)
- `BLOCK_4_PID(3,0.5,5).fig` — Full PID Kp=3 Ki=0.5 Kd=5
