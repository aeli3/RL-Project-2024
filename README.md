# SmartGrid-RL: Optimizing Battery Control with Reinforcement Learning

Welcome to the RL Project 2024 repository! This repository contains the code and assets for the Applied Reinforcement Learning Project – SmartGrid Battery Optimization, developed as part of a 2024 data science course.

The aim of this project is to build a reinforcement learning agent capable of optimizing the operation of an electric vehicle battery under dynamic electricity pricing and grid constraints. The project simulates real-world smart grid challenges using real electricity price data and adheres to strict operational and physical rules of battery use.

## Files

- **RL_Project(Own Environment).ipynb:** This notebook contains code related to the project using our custom environment.

- **RL_Project(Test Environment).ipynb:** This notebook contains code related to the project using a test environment.

## Project Setup and Environment
The goal of the project is to train a reinforcement learning agent that learns how to operate a 50kWh electric vehicle battery in a smart grid setting. The agent aims to minimize electricity costs by deciding when to charge or discharge the battery, based on hourly electricity prices and physical battery constraints. The model is trained on real electricity price data spanning three years.

The battery interacts with a dynamic electricity market. Electricity can be purchased at twice the spot price (to account for transmission fees and taxes) and sold at the regular market rate. The system must account for battery inefficiencies, capacity limits, and mandatory operational constraints—such as maintaining a minimum charge of 20kWh by 8:00 AM every day.

To solve this problem, we implemented a custom Gymnasium-compatible environment that accurately reflects the physical limitations of the battery and the structure of electricity prices. This environment only allows access to past and current prices, making it a suitable application for reinforcement learning instead of classical optimization.

## Dataset

Training and validation were performed using three years of historical hourly electricity price data. The dataset is provided in .xls format and includes timestamps and market prices in euros per MWh. The agent uses this data in real-time during training, without access to future values.

We begin with exploratory data analysis. We observe that the average price of electricity depends both on the time in the year (electricity is more expensive in colder months) and on the hour of the day (the prices are lowest around 4am and highest around 7 pm).

![hourly_averages_bymonth](https://github.com/user-attachments/assets/88a133bf-21b3-4677-870d-aa66f2ed785b)


## Baseline Strategy

As a starting point, we developed a baseline model based on a simple rule-based strategy. The baseline charges the battery during cheap night-time hours and discharges during expensive periods, while ensuring compliance with the required minimum charge constraint. This provided a useful benchmark to compare the performance of the reinforcement learning agent. A visualization of the behaviour of the agent is show below.

![random_agent_visualisation](https://github.com/user-attachments/assets/05288763-b988-41cd-b3db-b235598a0158)

## Reinforcement Learning Agent

The primary model in this project is a Q-learning agent that learns optimal battery control policies through interaction with the environment. We discretized the state and action spaces to enable tabular Q-learning and used an epsilon-greedy policy for exploration. The reward function was carefully designed to encourage profitability while heavily penalizing violations of physical and operational constraints.
Throughout training, we tracked the agent’s performance using episode rewards and battery operation logs. The model was evaluated on a separate validation dataset to test its generalizability.
A visualization of the behaviour of the agent is show below.

![dynamic_vis](https://github.com/user-attachments/assets/252d2efd-95fd-447e-84ae-766ff84697d3)


## Results

The Q-learning agent demonstrated improved performance over the baseline strategy, particularly in adapting to rapid fluctuations in electricity prices. It successfully learned to charge and discharge in response to market signals while respecting all safety constraints. Performance was measured in terms of total profit, stability of the policy, and adherence to operational rules.

The training profit is shown in the figure below. 

![tabular](https://github.com/user-attachments/assets/721eb50c-1452-4643-a3a5-33cd589a8964)


## Authors

- [Ali](https://github.com/aeli3) - Initial author and contributor.
- [Barbara](https://github.com/babura47) - Initial author and contributor.
- [Thomas](https://github.com/Jinobey) - Initial author and contributor.
