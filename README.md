# Human-like Longitudinal Control for Autonomous Driving

![C++](https://img.shields.io/badge/C%2B%2B-00599C?logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)

My part of the course project for **Intelligent Vehicles and Autonomous Driving**. The agent controls
a car's speed through **intersections and traffic lights**. Instead of following hand-written rules, it plans
**minimum-jerk motion primitives**, which produce smooth, human-like acceleration profiles.

---

## Approach

The controller is inspired by human sensorimotor behaviour:

- **Action priming:** generates candidate manoeuvres (affordances), following the *minimal intervention principle*.
- **Action selection:** picks the best candidate with a mechanism inspired by the *basal ganglia*.

Each manoeuvre is a closed-form **minimum-jerk primitive**: a quintic position profile defined by
the initial state (v₀, a₀) and the target distance, speed and time.

### Behaviours

| Scenario | Actions |
| --- | --- |
| **Intersection** | Stop at or before the stop line, **or** cross within a speed window while keeping a safe time gap to other vehicles |
| **Traffic light** | Stop at or before the light, **or** pass within a given time window and speed interval |

### Optimal control output

| Velocity / position profile | Primitive coefficients |
| --- | --- |
| ![Optimal Control](Optimal%20Control.png) | ![Coefficients](Coefficients%20of%20Optimal%20Control.png) |

## Repository contents

```
├── starting_point.cc        # Agent main loop: receives scenario messages, sends manoeuvres
├── agent_functions.hpp      # Stop / pass primitives, optimal time & velocity, low-level control
└── pass_primitive_plot.py   # Plots the velocity and position profiles from logged coefficients
```

Key functions in `agent_functions.hpp`:

- `stopPrimitive`: minimum-jerk stop at distance `sf`
- `Passprimitive` / `Passprimitve_with_j0`: pass within `[Vmin, Vmax]` and `[Tmin, Tmax]`
- `choose_m_star`: selects the primitive to execute
- `LowLevelControl`: converts the primitive into an acceleration command (with saturation)

> **Note:** This repository contains only the parts I wrote. The simulator, server library and the
> other team members' code are not included, so it will not build on its own. Contact me if you
> would like more details.

## Tech stack

C++ · Python · NumPy · Matplotlib · Optimal control · Motion primitives

## Author

**Yogeswaran Amsavalli** · [GitHub](https://github.com/YogiOnCode)
