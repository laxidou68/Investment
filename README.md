# Investment
As quantitative strategies are studied in depth, many previously very effective factors, such as market capitalization factor, momentum factor, volatility factor, etc., sometimes experience more pronounced oscillations or failures . Therefore, the factor selection models need to be further improved. In this report, an attempt was made to combine the equal weighted sum of the effective factors for stock selection with a hedging strategy for the pushing stock index, in order to obtain a better performing strategy. More experimentation and research on factor selection is needed in the future.
This report is divided into the following main sections.
1. First, we introduce common indicators for factor selection to build a factor library
2. Secondly, the new factor is constructed using equal weight summation for stock selection, as a long strategy
3. Then, we construct the CSI 500 stock index trade based on the component trading information and use it as a short strategy
4. Next, stock selection and timing are combined as the final trading strategy and evaluated for the strategy
5. Finally, performance attribution, i.e., analysis of stock selection returns and timing returns

I. One-factor backtesting and factor library building
Using 5Dforward as an example for backtesting, the strategy is evaluated by quintiles of the stock pool and some of the results are listed below
![text]


Based on the above strategy performance, information such as decreasing 5D forward factor return grouping, higher overall volatility, and maximum pullback data such as "Now, 2011" can be found. Similarly, the 16 factors with the best return performance were selected as the factor pool according to the single factor backtest and strategy performance.

II. Factor selection
2.1 Factor selection based on IC value analysis
The IC of the factor is the correlation coefficient between the exposure vector of the factor in period T and the stock return vector in period T+1, i.e.
ICT = corr(rT+1, XT)
The factor exposure vectors in the above equation are generally not used directly from the original factor values, but from the factor values after depolarization and neutralization. In practice, the Pearson correlation coefficient may be more influenced by the extreme values of the factors, while the Spearman rank correlation coefficient is more robust. The IC computed in this way is generally called Rank IC.
The IC value analysis model is constructed as follows.
1. The stock pool, the return interval, and the cross-sectional period are the same as the regression method.
2. The factor exposure vector is pre-processed and the Spearman's rank correlation coefficient of the T-period factor exposure vector and the T+1-period stock return vector is calculated as the T-period factor Rank IC value.
The IC value is calculated based on the weekly turnover rate, and the top 6 best performing factors are selected based on the size of the IC value.
![text]


A sliding window is set at the end of each year to select the top 6 performing factors from the factor pool for each year.
![text]


2.2 Equal weight summation of factors
That is, each factor is given the same weight , and its weight vector is
V = (1/M, 1/M, .... , 1/M)
This weighting approach is simpler, but does not take into account the differences in factor validity.
![text]

2.3 Factor Selection
Decile the stock pool and select the top 30 stocks to go long.
![text]
Set monthly position transfers.
![text]

2.4 Strategy Evaluation
![text]
Based on the strategy evaluation, it is clear that the maximum retracement of the factor stock selection strategy is large and also the annualized volatility is high, so further improvement is needed.

III. the broad market strategy
3.1 Data sources
CSI 500 stock index and constituent trading data are sourced from the JoinQuant platform and Wind.
![text]

3.2 Indicator construction
First set the stock stop threshold µ (temporarily set to 9.5%)
Stocks up > µ , limit up;
Stocks up < - µ , limit down
a) Indicators based on the comparison of long and short market forces in a single day
Ratio of limit up: The ratio of the number of constituent stocks with a single day increase greater than µ to the total number of its constituent stocks in a broad-based index.
Ratio of limit down: The ratio of the number of components of a broad-based index with a one-day decline greater than µ (one-day increase less than - µ) to the total number of its components.
Push ratio: Up ratio - down ratio ([ -1, 1]).
![text]

b) Indicator based on the comparison of long and short market forces for two consecutive days
Consecutive ratio of limit up: the ratio of the number of stocks that are up > µ to the total number of its components for both today's and yesterday's increases in the broad-based index
Continuous Ratio of limit down: The ratio of the number of stocks whose broad-based index is down > µ (up less than -µ) to the total number of its constituents for both today's and yesterday's declines
Scissors of consecutive board ratios: consecutive up ratio - consecutive down ratio ([-1, 1]).
Code.
![text]

c) Indicator based on yesterday's closing price and the highest and lowest price
Floor-to-sky ratio: The ratio of the number of stocks in the broad-based index with today's floor trend to the total number of its components; where the floor trend is the lowest price today compared to yesterday's closing price of less than - µ (the stock has fallen during the session), while today's closing price compared to yesterday's closing price of more than µ (the last closing is up).
Sky-to-Floor Ratio: The ratio of the number of stocks in the broad-based index with a sky floor today to the total number of its components; of which, the sky floor stock trend: today's highest price compared to yesterday's closing price rose more than µ (the stock has been stopped during the day), but today's closing price compared to yesterday's closing price rose less than - µ (the last closing was a stop)
Floor-to-sky ratio scissors: Floor-to-sky ratio - Sky-to-floor ratio.
![text]

Price Volume Resonance Timing Model.
Long position: AMA30/AMA100 of the above three indicators > 1.15, and AMA30 and AMA100 are greater than 0.  Short position: AMA30 or AMA100 is less than 0
Transformation of buy and sell signals based on timing models for each indicator, e.g.
![text]

d) Construct the final stock index buy and sell signals by summing the factors with equal weights.
![text]

3.3 Strategy Evaluation
![text]
The push model worked well for the CSI 500 stock market after 2016, able to outperform the broader market and achieve a perfect bottoming and topping. However, before February 2016, there was a partial probability of losing the bottoming signal, and also failed to capture some of the tops and bottoms of the market.
![text]
The push model works better for the CSI 300 in the backtest period overall, specifically, it performs poorly in 2009-2012, which is consistent with the CSI 500, and can outperform the broader market in the rest of the period, which is perfect for bottoming and topping out.
In addition, the performance of the model in different markets is shown in Table 1 below.
![text]
Based on the calculation of the indicators, we can see that the overall performance of the PUSH Timing System on the CSI 300 is better, as evidenced by the lower annualized volatility, higher Sharpe Ratio, Information Ratio and Winning Ratio.

IV. hedging stock index strategy
Factor selection combined with pushing the broad market timing to build a stock index hedging strategy, the broad market selection of the CSI 300, the strategy performance is as follows.
![text]
![text]
The introduction of hedging has improved the performance of the strategy to some extent, as the hedging has reduced the volatility and increased the information ratio, but also reduced the annualized return.

V. Performance Attribution
![text]
7.45% of the gains in the hedge-push CSI 300 stock index system came from timing trades, with the remaining gains coming from factor selection trades
