# Quantitative Stock Selection Based on Stock Index Hedging

As quantitative strategies are studied in depth, many previously very effective factors, such as market capitalization factor, momentum factor, volatility factor, etc., sometimes experience more pronounced oscillations or failures . Therefore, the factor selection models need to be further improved. In this report, an attempt was made to combine the equal weighted sum of the effective factors for stock selection with a hedging strategy for the pushing stock index, in order to obtain a better performing strategy. More experimentation and research on factor selection is needed in the future.

This report is divided into the following main sections.
1. First, we introduce common indicators for factor selection to build a factor library
2. Secondly, the new factor is constructed using equal weight summation for stock selection, as a long strategy
3. Then, we construct the CSI 500 stock index trade based on the component trading information and use it as a short strategy
4. Next, stock selection and timing are combined as the final trading strategy and evaluated for the strategy
5. Finally, performance attribution, i.e., analysis of stock selection returns and timing returns

I. One-factor backtesting and factor library building
Using 5Dforward as an example for backtesting, the strategy is evaluated by quintiles of the stock pool and some of the results are listed below
