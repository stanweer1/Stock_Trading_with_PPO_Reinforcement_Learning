# Stock_Trading_with_PPO_Reinforcement_Learning

## Overview

This project aimed to develop and evaluate an autonomous trading agent using a Proximal Policy Optimization (PPO) reinforcement learning model. The agent was trained on historical stock price data for Gamestop (GME) to learn a trading strategy. The goal was to maximize its portfolio value by making intelligent buy or sell decisions.

## Methodology

1.  The `gym-anytrading` library was used to create a custom trading environment based on historical GME stock data from yfinance. A lookback window of 10 days was configured, allowing the agent to consider the last 10 data points before making a decision at each step.

2.  A Proximal Policy Optimization (PPO) agent was implemented using the `stable-baselines3` library. PPO is a state-of-the-art reinforcement learning algorithm known for its stability and performance. 

3.  When the model predicted a 'Buy' action, it invested 20% of its current cash balance to purchase shares at the current market price. When the model predicted a 'Sell' action, it liquidated all of its currently held shares.

## Results

The agent was evaluated on the historical data following the training phase. The performance was exceptional, turning the initial investment into a multi-million dollar portfolio.

### Performance Metrics

* **Initial Balance**: `$100,000.00`
* **Final Portfolio Value**: `$160,571.61`
* **Total Profit**: `$60,571.61`
* **Return on Investment**: `60.57%`
* **Total Buy Actions**: `962`
* **Total Sell Actions**: `147`

## Analysis and Conclusion

A key behavioral characteristic of the trained policy is its high trading frequency, with 962 buy actions and 147 sell actions over the evaluation period. Because each buy action allocates a fixed fraction (20%) of the remaining balance rather than committing all capital, the agent effectively implements a progressive scaling-in strategy, accumulating positions across multiple buy signals before eventually liquidating. This results in a form of implicit risk diversification over time, as capital is not deployed in a single entry point.

The portfolio value curve shows extended periods of growth punctuated by sharp changes coinciding with major GME price movements. These transitions suggest that the agent is not merely following a static trend-following rule, but is responding to short-term temporal patterns captured within the 10-day observation window. PPO’s clipped objective likely contributed to training stability, preventing destructive policy updates despite the highly volatile nature of GME during the selected time horizon.

However, it is important to note that the reported performance reflects in-sample evaluation on the same data distribution used during training. As a result, the observed profitability should be interpreted as evidence of the agent’s capacity to fit historical dynamics, rather than proof of deployable trading skill in real markets. 

**Limitations and Future Work:**
    1.  The buy/sell logic assumes instantaneous execution at the observed close price with infinite liquidity, which is unrealistic in practice. 
    2.  Training and evaluation occur on overlapping data, introducing look-ahead bias and inflating apparent performance. 
    3.  The agent was trained and evaluated on one highly anomalous stock (GME), whose dynamics during this period are not representative of typical equity behavior. 
    4.  The environment assumes frictionless trading. Given the extremely high number of trades, even modest transaction fees would significantly erode returns and could fully negate profitability.

* **Next Steps**: To create a more robust agent, future work should involve:
    1.  Training the model on more diverse data, including market downturns and periods of high volatility.
    2.  Engineering a more sophisticated reward function that penalizes unrealized losses or rewards successful profit-taking (selling higher than the purchase price).
    3.  Implementing more complex trading logic, such as partial sells or stop-loss orders.
    4.  Out-of-sample and walk-forward validation to assess generalization across unseen market regimes.
