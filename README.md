# Campus Rumour Spreading Simulation

**An agent-based model, built in NetLogo, of how a rumour moves through a student population and how fact-checking slows it down.**

![NetLogo](https://img.shields.io/badge/NetLogo-7.0.4-blue) ![Method](https://img.shields.io/badge/method-Agent--Based%20Modelling-orange) ![Type](https://img.shields.io/badge/type-academic%20project-green)

---

## 1. Problem Statement

On a college campus, a rumour (an exam leak, a cancelled class, a fake circular) can reach hundreds of students within hours. No one person decides how far it goes. The outcome comes from thousands of small, local events: two students meet, one tells the other, and the listener either believes it or not. Some students stop and check the facts; once they do, they stop passing the rumour on.

These small events are hard to reason about with equations alone, because the result depends on who happens to meet whom. This project therefore uses **Agent-Based Modelling (ABM)**: each student is simulated as an individual agent with simple rules, and the campus-wide pattern of spread is observed as it *emerges* from those rules.

The central question is:

> **How do the chance of passing a rumour on, the chance of fact-checking it, and the starting conditions (population size and number of initial believers) decide how far and how fast a rumour spreads across a campus?**

Sub-questions the model is designed to explore:

1. How does a higher **spread probability** change the speed and peak of the rumour?
2. How much **fact-checking** is needed to stop the rumour before it reaches most students?
3. Does a **denser campus** (more students in the same space) make the rumour spread more easily?
4. Do **more initial believers** change the final outcome, or only how quickly it is reached?

## 2. Approach: Agent-Based Modelling

| ABM concept | How it appears in this model |
|---|---|
| Agents | Students (NetLogo *turtles*) |
| Environment | A 33 × 33 patch campus that wraps around at the edges |
| Agent state | `rumor-status`: `unaware`, `believer` or `verified` |
| Local interaction | Believers can only influence students within a radius of **1.5** patches |
| Stochastic rules | Spreading and fact-checking each happen with a set probability |
| Emergence | The campus-wide spread curve is never programmed; it arises from individual encounters |

The model is related to the classic **SIR epidemic model** and the **Daley–Kendall rumour model**:

| This model | SIR equivalent | Rumour-model equivalent |
|---|---|---|
| Unaware | Susceptible | Ignorant |
| Believer | Infected | Spreader |
| Verified | Recovered | Stifler |

The key difference is that here a believer becomes "verified" by checking the facts on their own (a fixed chance each tick), not by meeting other people who already know the rumour.

## 3. Model Description

### Agent states

| State | Colour in the view | Meaning |
|---|---|---|
| `unaware` | Sky blue | Has not heard or not accepted the rumour |
| `believer` | Orange | Believes the rumour and passes it to nearby students |
| `verified` | Green | Has fact-checked the rumour and no longer spreads it |

State changes only go one way: **unaware → believer → verified**. A verified student never becomes a believer again.

### What happens in each tick

Each call of `go` is one tick (one time step):

1. **Move:** every student turns by a random angle (a random right turn of 0–49° then a random left turn of 0–49°) and walks forward 0.5 patches. This gives a random walk around the campus.
2. **Spread:** every student who was a believer at the start of this step looks at all students within radius 1.5. Each `unaware` one becomes a `believer` with probability `spread-probability` %.
3. **Fact-check:** every current believer, including students who were converted in step 2, becomes `verified` with probability `fact-check-probability` %.
4. The tick counter advances.

### Initialisation (`setup`)

- `population` students are placed at random positions, all `unaware`.
- `initial-believers` of them are chosen at random and set to `believer`.

## 4. Parameters (Interface sliders)

| Slider | Range | Step | Default | Effect |
|---|---|---|---|---|
| `population` | 50 – 500 | 50 | 200 | Number of students; with a fixed campus size this also sets **density** |
| `initial-believers` | 1 – 20 | 1 | 4 | Students who already believe the rumour at tick 0 |
| `spread-probability` | 0 – 100 % | 5 | 20 | Chance an unaware student nearby is convinced, per believer, per tick |
| `fact-check-probability` | 0 – 100 % | 5 | 10 | Chance a believer checks the facts each tick and stops spreading |

Fixed values in the code: interaction radius = **1.5** patches, step length = **0.5** patches, world = 33 × 33 patches with wrapping.

## 5. How to Run

1. Install **NetLogo 7.0.4 or later** from [ccl.northwestern.edu/netlogo](https://ccl.northwestern.edu/netlogo/). The `.nlogox` file format needs NetLogo 7.
2. Clone this repository:
   ```bash
   git clone https://github.com/earth-bhumi22/campus-rumour-spreading-simulation.git
   ```
3. Open `Campus_Rumour_Simulation.nlogox` in NetLogo.
4. Set the four sliders.
5. Click **SETUP** to place the students.
6. Click **GO** to start the simulation. Click it again to pause.
7. Watch the colours change: blue students turn orange as they hear the rumour, and orange students turn green as they fact-check.

> **Note:** the simulation does not stop by itself. Once no orange (believer) students are left, nothing more can change, so pause it with **GO**.

## 6. Suggested Experiments

Change one slider at a time and keep the others at their defaults. Because the model is random, run each setting several times and compare the typical outcome rather than a single run.

| # | Experiment | Change | What to observe |
|---|---|---|---|
| 1 | Fast-spreading rumour | `spread-probability` 20 → 60 | How quickly orange takes over; how many students stay blue |
| 2 | Strong fact-checking culture | `fact-check-probability` 10 → 40 | Whether the rumour dies out early |
| 3 | Crowded vs. empty campus | `population` 50 → 500 | Whether density alone changes how far the rumour gets |
| 4 | Bigger initial leak | `initial-believers` 1 → 20 | Whether the final reach changes, or only the speed |
| 5 | Weak rumour | `spread-probability` 20 → 5 | Whether the rumour fades before it spreads |
| 6 | Tipping point | Keep `spread-probability` fixed, raise `fact-check-probability` step by step | The value at which the rumour stops reaching most of the campus |

Useful measures to record for each run:

- **Final reach:** the number of students who ever heard the rumour (orange + green at the end)
- **Peak believers:** the largest number of orange students at any one time, and the tick it happened
- **Duration:** the number of ticks until no believers are left
- **Untouched students:** the number of blue students left at the end

## 7. Assumptions and Limitations

This is a simplified teaching model, not a prediction of real student behaviour.

- Every student follows the same rules. Nobody is more gullible, more sceptical or better connected than anyone else.
- Contact depends only on physical closeness during a random walk. There are no friendships, hostels, classes or WhatsApp groups.
- Fact-checking is a fixed random chance. It is not triggered by evidence, by peers or by official announcements.
- "Verified" means the student stopped spreading the rumour. The model does not decide whether the rumour is actually true.
- Updates within a tick happen in order (move, then spread, then fact-check), so a student can be convinced and fact-check in the same tick.
- The model has not been calibrated against real campus data.

## 8. Possible Extensions

- Plots and monitors for the number of unaware, believer and verified students over time
- A stop condition when no believers remain
- A **BehaviorSpace** experiment to sweep parameters and export results to CSV
- Social-network contacts (friend groups, classes) in place of or alongside spatial contact
- Individual differences in trust and scepticism
- Stifling through contact: a believer who meets a verified student stops spreading
- Verified students actively correcting believers they meet
- Two competing messages: the rumour and an official clarification

## 9. Repository Structure

```
campus-rumour-spreading-simulation/
├── Campus_Rumour_Simulation.nlogox   # NetLogo model (code + interface)
└── README.md                         # This file
```

## 10. References

- Wilensky, U. (1999). *NetLogo*. Center for Connected Learning and Computer-Based Modeling, Northwestern University. http://ccl.northwestern.edu/netlogo/
- Daley, D. J., & Kendall, D. G. (1964). Epidemics and rumours. *Nature*, 204, 1118.
- Kermack, W. O., & McKendrick, A. G. (1927). A contribution to the mathematical theory of epidemics. *Proceedings of the Royal Society A*, 115(772), 700–721.
- Wilensky, U., & Rand, W. (2015). *An Introduction to Agent-Based Modeling*. MIT Press.

## Authors

- **Bhumi Kansal** ([earth-bhumi22](https://github.com/earth-bhumi22))
- **Nikhil Maurya** ([nikhil23maurya](https://github.com/nikhil23maurya))

Academic project, B.Tech Computer Science and Engineering (2nd Year), Faculty of Technology, University of Delhi, 2026.
