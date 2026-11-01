# Campus Rumour Spreading Simulation

### An Agent-Based Modelling Project Using NetLogo

A NetLogo-based agent-based simulation that explores how rumours propagate through a population of students in a campus environment and how individual fact-checking behaviour influences the spread of information.

The project demonstrates how simple individual interactions can collectively produce complex patterns of information diffusion.

---

## Project Overview

Rumours can spread rapidly through social interactions, particularly in environments where individuals interact frequently.

This project uses **Agent-Based Modelling (ABM)** to simulate the behaviour of students as independent agents who move around a virtual campus, communicate with nearby individuals, and potentially change their beliefs.

The simulation examines how factors such as transmission probability, initial believers, population size, and fact-checking probability influence the overall propagation of a rumour.

## Objectives

- Understand the fundamental principles of Agent-Based Modelling.
- Simulate information propagation through local agent interactions.
- Examine the role of probabilistic behaviour in rumour transmission.
- Explore how individual fact-checking affects rumour propagation.
- Visualize the collective behaviour emerging from simple agent-level rules.

## Technologies Used

| Technology | Purpose |
|---|---|
| NetLogo | Agent-based simulation environment |
| NetLogo Programming Language | Agent behaviour and simulation logic |
| Agent-Based Modelling | Computational modelling methodology |

## Simulation Model

Each student is represented by an autonomous agent, called a **turtle** in NetLogo.

Agents move around a two-dimensional virtual campus and interact with nearby students.

### Agent States

| State | Colour | Description |
|---|---|---|
| Unaware | Blue | Student has not adopted the rumour |
| Believer | Orange | Student believes the rumour and can spread it |
| Verified | Green | Student has performed fact-checking and stops spreading the rumour |

### Behavioural Rules

**1. Initialization**

A specified number of students are generated at random positions. A selected group begins as initial rumour believers, while the remaining students are unaware.

**2. Student Movement**

Students move independently around the simulation environment using randomized turns and forward movement.

**3. Rumour Transmission**

A believer can transmit the rumour to an unaware student within a defined interaction radius.

Transmission is probabilistic and depends on the configured spread probability.

**4. Fact-Checking**

Believers have an independent probability of fact-checking the rumour during each simulation step.

After fact-checking, they enter the verified state and stop spreading the rumour.

**5. Simulation Progression**

The simulation advances through discrete time steps, represented by NetLogo ticks.

## Simulation Parameters

| Parameter | Description |
|---|---|
| `population` | Total number of student agents |
| `initial-believers` | Number of initial rumour believers |
| `spread-probability` | Probability (%) of rumour transmission during an eligible interaction |
| `fact-check-probability` | Probability (%) that a believer fact-checks during a simulation step |

The model uses an interaction radius of 1.5 NetLogo units and a movement step of 0.5 units.

## How to Run

1. Download and install NetLogo from [netlogo.org](https://www.netlogo.org/).
2. Clone or download this GitHub repository.
3. Open the project model file using NetLogo.
4. Configure the simulation parameters using the Interface controls.
5. Click **Setup** to initialize the student population.
6. Click **Go** to start the simulation.
7. Observe how the agents change their states as the simulation progresses.

**Note:** The number of initial believers must not exceed the total population.

## Experiments and Observations

The simulation can be used to explore different scenarios:

**Scenario 1 — High Rumour Transmission**

Increase spread probability to examine how quickly information can propagate through the population.

**Scenario 2 — Increased Fact-Checking**

Increase fact-check probability to observe how the conversion of believers into non-spreading agents affects rumour propagation.

**Scenario 3 — Different Initial Conditions**

Modify the population and number of initial believers to explore how starting conditions influence the simulation.

**Scenario 4 — Low Interaction-Based Transmission**

Reduce spread probability to observe how weaker transmission affects the diffusion process.

These are exploratory experiments rather than empirically validated predictions of real student behaviour.

## Model Limitations

This is a simplified computational model developed for educational purposes.

- All students follow the same behavioural rules.
- Interactions depend on spatial proximity rather than real social networks.
- Fact-checking is represented probabilistically rather than through detailed information evaluation.
- The verified state represents fact-checking and cessation of spreading; the model does not independently establish whether the rumour is true or false.
- The simulation is not calibrated against real-world campus data.

## Future Enhancements

Potential improvements include:

- Realistic friendship and social-network structures.
- Different trust levels and influence among students.
- Agent-specific transmission and fact-checking behaviour.
- Real-time statistical charts for agent populations.
- Multiple competing rumours.
- Data export and comparative simulation experiments.

## Academic Relevance

This project demonstrates several fundamental concepts of Agent-Based Modelling:

- Autonomous agents
- Local interactions
- Probabilistic state transitions
- Dynamic simulation environments
- Emergent collective behaviour

It provides a practical introduction to computational social simulation and information diffusion.

---

**Project Type:** Academic / Educational Simulation

**Domain:** Agent-Based Modelling and Computational Social Systems

**Platform:** NetLogo
