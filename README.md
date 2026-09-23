# derivatives-pricing-toolkit
A small Python toolkit implementing three core quantitative finance models used to price options and futures contracts.

What it does

The toolkit contains three independent pricing functions:

Monte Carlo Simulation — simulates thousands of possible future price paths for an underlying asset and uses the average outcome to estimate its expected price at maturity.
Black-Scholes Model — calculates the theoretical price of a European call option using the closed-form Black-Scholes formula.
Cost-of-Carry Model — calculates the fair price of a futures contract based on the spot price, risk-free rate, and storage costs.
How it works
Monte Carlo Simulation

Generates 10,000 simulated price paths over the life of the contract using Geometric Brownian Motion, the standard model for how asset prices move randomly over time under a given expected return (drift) and volatility. Each path is simulated day-by-day (252 steps, matching trading days in a year), and the average simulated price at maturity is taken as the estimated fair value.

Black-Scholes Model

Uses the spot price, strike price, risk-free rate, volatility, and time to maturity to calculate d1 and d2 (intermediate terms capturing the probability-adjusted expected payoff), then applies the cumulative normal distribution to price a European call option.

Cost-of-Carry Model

Calculates the fair futures price by compounding the spot price forward at the combined rate of the risk-free rate and storage cost over the contract's life — reflecting the fact that holding a physical commodity to deliver later carries a financing and storage cost.

Tech stack
Python
numpy — numerical computation and vectorised simulation
scipy.stats — cumulative normal distribution for Black-Scholes
Example output

For a commodity priced at $1.20 with 25% volatility, a 2% risk-free rate, and 6 months to maturity:

The average simulated price of the coffee futures contract at maturity is $1.213.
The price of the call option is $0.083.
The fair price of the coffee futures contract is $1.218 per pound.
Running it
bash
pip install numpy scipy
python financial_models.py

All three models run automatically and print their results. Parameters (spot price, strike, volatility, rate, time to maturity) can be edited at the top of each function.

Why three models together

Each model answers a related but distinct pricing question:

Monte Carlo estimates expected price under uncertainty by simulating many possible outcomes.
Black-Scholes gives a single, closed-form theoretical price for an option, assuming the same underlying price dynamics.
Cost-of-carry prices a futures contract from a no-arbitrage argument, independent of simulating price paths at all.

Implementing all three side by side was a useful way to compare a simulation-based approach against closed-form analytical solutions for related pricing problems.

Limitations & possible extensions
Assumes constant volatility and risk-free rate, which real markets do not have.
Black-Scholes only prices European-style options (exercisable only at maturity); American-style options would need a different model.
Could be extended with put option pricing, Greeks (delta, gamma, vega) calculations, or a comparison against real market option prices.
