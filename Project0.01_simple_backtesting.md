# Simple strategy backtester

### The goal of this project is simple, I am looking to understand the process of cleaning data, computing returns and descriptive statistics, computing signals and running a backtest. Basically understanding the pipeline of how strategies are tested and evaluated, there are a lot of technical details that I want to look into and understand better, but before that I wanted to understand how the raw process works without going into too much detail.

#### This project is simply one where i use a simple moving average crossover as my strategy, run a backtest and compare it to buy and hold the same stock. Finally providing performance metrics of both strategies 

#### I will divide the project into 6 sections
1. Data cleaning and preparation
2. Computing returns and descriptive statistics
3. Computing signals
4. Running a backtest
5. Comparing the strategy to buy and hold
6. Providing performance metrics

#### And finally talk about limitations, where there will definitely be a lot, and also the ways to improve which will give me the direction for my next project 


## Section 1: Data cleaning and preparation 
We begin by importing the data from yfinance, check the descriptive statistics, and perform 3 checks for data quality:
1. Check for missing values
2. Check for Zero volume days
3. Check for duplicate dates

Finally plot the adjusted close price and volume graph 

## Section 2: Returns & Statistics 
In this section we compute both the simple returns and log returns, to see the difference and understand that due to log returns being time additive, it is often preferred for statistical modelling,

Then we compute the descriptive statistics of both returns and plot both the distribution of returns and the cumulative returns 

## Section 3: Technical indicators
This is where we compute the indicators that will feed into section 4 and 5 for the backtesting process

We will compute the following indicators:
1. Simple Moving Average of 50 days (SMA_50)
2. Simple Moving Average of 200 days (SMA_200)

$$ SMA_t = \frac{1}{n} \sum_{i=0}^{n-1} P_{i} $$
- where $n$ is the number of days, 
- $P_i$ is the price of the stock on day i

3. Relative strength index (RSI) of 14 days

$$ RSI_t = 100 - \frac{100}{1 + RS_t} $$
- where $RS_t$ is the relative strength of the stock on day t

A plot will be made for each of them, where for the RSI we set the boundaries at 30 and 70

## Section 4: Creating signals
In this section we will create the signals for the strategy, which will be used to generate the trades in the backtest

The strategy is as follows:

- Buy/hold when short-term trend > long-term trend
- Not buy/Sell when short-term trend < long-term trend
- Where short-term trend is SMA_50 and long-term trend is SMA_200

**Note:** to avoid lookahead bias, we create another column, "position", which will shift by one row down, this way when "postition" changes from 0 to 1, we make sure that the trade is executed on the next day

Finally we will plot the signals on the price chart, as well as the times we hold the stock
- Every green triangle mark every entry point
- Every red triangle mark every exit point

## Section 5: Running the backtest


In this section we will run the backtest, which will generate both the strategy returns and the buy and hold returns, as well as a plot of the drawdown over time 

We will use the following formulas:

$$ Str_r = Position_t\times R_t $$

- $Str_r$ is the strategy return on day t
- $Position_t$ a dummy variable, if 1 buy/hold, if 0 not buy/sell
- $R_t$ is the return of the stock on day t

$$ DD_t= \frac{Str_t-peak_t}{peak_t} \times 100 $$

- $DD_t$ is the drawdown on day t
- $Str_t$ is the cumulative return of the strategy on day t
- $peak_t$ is the peak cumulative return of the strategy on day t

**Note:** we converted the returns to dollar growth by assuming a starting capital of $1

## Section 6: Performance metrics 
In this section we will go over the results that we got and compute different metrics to evaluate the performance of the strategy

We will compute the following metrics:
1. Annualised Return
2. Annualised Volatility
3. Sharpe Ratio
4. Maximum Drawdown
5. Calmar Ratio
6. Win Rate (strategy only)
7. Time in Market (strategy only)




## Limitations & Possible improvements 
This is where I will outline  the various limitations of this project and the possible improvements that can be made, which will give me the direction for my next project

- Single asset
- No measure of predictive power 
- No statistical significance testing
- Fixed arbitrary thresholds
- In-sample testing only
- Binary signals
- No regime awareness
- Single time Horizon 

These are the some of the limitations of this project and I will reading around to see how to improve on them, which will give me the direction for my next project
