---
layout: post
title:  "Electricity Demand-Production Optimization Agent"
date:   2024-12-08 23:04:50 -0500
categories: jekyll update
---
Language: Python 3
<br>
Tools: pandas, numpy, matplotlib,Jupyter Notebook
<br>
Data Resouce: https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption/data
<br>
Project Purpose
<br>
Balancing electricity supply and demand is a real problem in the world. Inefficiencies cause energy waste and high costs for the users. This project want to create a flexible electricity pricing system using Q-Learning to improve pricing decisions, reduce imbalances, and cut down on energy using.
<br>
<br>
What Was Accomplished
1. Data Preprocessing:
Combined multiple regional energy consumption datasets into a one dataset.
Simulated supply-side variables by Wind production, Solar production,Fossil production to increase complexity. However, these were combined into a single unified "supply" index, and individual components were not directly utilized in the final model. Maybe I can try to use them for future/more diffcult work.
I use dynamic randomness to supply to simulate real-world uncertainties. I set up a initial price as 100.
<br>
2. State and Action Definitions:
States: In the project, the state space was discretized into 10 states, reflecting the supply-demand relationship. The state is defined by the imbalance between supply and demand. The imbalance (Imbalance = Supply - Demand) was seperate to 10 levels equal-width bins.
Agent Actions:
Increase Price (+10%)
Decrease Price (-10%)
Hold Price (No change)
<br>
3. Reward Function:
Encouraged:
Balanced supply and demand (abs(imbalance) < 200).
Reasonable pricing (80 <= price <= 150).
Penalized:
big imbalances.
<br>
4. Implementation of Q-Learning:
Created a Q-Learning agent to make pricing decisions based on states.
Used the learning_rate=0.1, discount_factor=0.8, exploration_rate=1.0 for the agent.
Updated Q-values using the Temporal Difference (TD) method.
<br>
5. Training and Analysis:
Because the dataset is 64MB which is too large, so I only use the first 2000 rows as training target which makes the agent faster 
Due to the dataset's size of 64MB, I limited the training to the first 2000 rows. This makes a faster processing and improved the agent's training efficiency. You can change the number of data to train when you reproduce it.
I trained the agent over 100 episodes.

How Success Was Measured/Project result:

Total Reward: Evaluated the cumulative reward across all time steps in each episode. Because each execucation which generate new data, for me the initial episodes showed a total reward of 53480. Over time, the rewards fluctuated but gradually improved. At the end, it shows a improvement compared to the earlier episodes.(number depending on the data you generate on your local machine)
Price Change: Price remained within the a range, typically between 80 and 150 units, aligning with the designed reward function.
Supply-Demand Imbalance: It shows a reductions in imbalance over training episodes.
Evaluation Results:

The Total Reward started small but increase after, indicating the agent learned to make more balanced pricing decisions.
Supply-demand imbalances were reduced in later episodes, showing the effectiveness of dynamic pricing.

