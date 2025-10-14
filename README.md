# Stock_Trading_with_PPO_Reinforcement_Learning

## Overview

This project aimed to develop and evaluate an autonomous trading agent using a Proximal Policy Optimization (PPO) reinforcement learning model. The agent was trained on historical stock price data for Apple Inc. (AAPL) to learn a trading strategy. The goal was to maximize its portfolio value by making intelligent buy or sell decisions.

## Methodology

1.  The `gym-anytrading` library was used to create a custom trading environment based on historical AAPL stock data from the `AAPL.csv` file. A lookback window of 10 days was configured, allowing the agent to consider the last 10 data points before making a decision at each step.

2.  A Proximal Policy Optimization (PPO) agent was implemented using the `stable-baselines3` library. PPO is a state-of-the-art reinforcement learning algorithm known for its stability and performance. 

3.  When the model predicted a 'Buy' action, it invested 20% of its current cash balance to purchase shares at the current market price. When the model predicted a 'Sell' action, it liquidated all of its currently held shares.

## Results

The agent was evaluated on the historical data following the training phase. The performance was exceptional, turning the initial investment into a multi-million dollar portfolio.

### Performance Metrics

* **Initial Balance**: `$100,000.00`
* **Final Portfolio Value**: `$3,961,377.50`
* **Total Profit**: `$3,861,377.50`
* **Return on Investment**: `3861.38%`
* **Total Buy Actions**: `3,763`
* **Total Sell Actions**: `0`

## Analysis and Conclusion

The results are, on the surface, spectacular. A nearly 4000% return is an incredible outcome. However, a deeper look at the agent's behavior is crucial.

The most striking observation is that **the agent never learned to sell**. It executed 3,763 buy actions and 0 sell actions. This means the agent's learned strategy was essentially an aggressive "buy-and-hold" or "buy-the-dip" strategy.

This approach was highly effective because the training and evaluation period (roughly 2009-2024) coincided with one of the most significant and sustained bull markets in history for AAPL stock. In an environment of consistent upward momentum, continuously buying and holding is an optimal strategy.

**Limitations and Future Work:**

* **Overfitting to Bull Market**: The model is likely overfitted to the specific historical data of a bull market. Its performance in a sideways or bear market would likely be poor, as it has not learned to take profits or cut losses by selling.
* **Reward Signal**: The environment's default reward structure may have implicitly favored holding assets over selling, as the asset's value generally increased over time.
* **Next Steps**: To create a more robust agent, future work should involve:
    1.  Training the model on more diverse data, including market downturns and periods of high volatility.
    2.  Engineering a more sophisticated reward function that penalizes unrealized losses or rewards successful profit-taking (selling higher than the purchase price).
    3.  Implementing more complex trading logic, such as partial sells or stop-loss orders.
