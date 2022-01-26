# LP strategies

Last updated on 01/26/2022.

This dataset consists of the daily token price, reserve, and volume data of 16 different WETH pools in Sushiswap, from 09/14/2020 to 01/26/2022.
The list of tokens is as follows:

- BAND
- COMP
- DAI
- LINK
- REN
- SNX
- SRM
- SUSD
- SUSHI
- UMA
- USDC
- AMP
- AMPL
- CRV
- USDT
- YFI

The dataset has two versions, `train` and `test`.
The `train` dataset spans from 09/14/2020 to 10/31/2021 whereas the `test` dataset contains the whole dataset, which means that the data from 11/01/2021 to 01/26/2022 can be only accessed within the `test` dataset.
I did this just to avoid the look-ahead bias.

Period | Frequency | Start Date | End Date | Samples
:--:|:--:|:--:|:--:|:--:
Training | Daily | 09/14/2020 | 10/31/2021 | 413
Testing | Daily | 11/01/2021 | 01/26/2022 | 87


The `observables` are the daily token price, reserve, and volume for each token, which leads to a total of 3 x 16 = 48 columns.
The `targets` are the estimated daily returns for each token pool, which was calculated by the following:

$$
\begin{align*}
\text{Total Return (\%)} &= \text{Trading Fee (\%)} + \text{Impermanent Loss (\%)} \\
&= \text{Fee Rate} \times \sqrt{\text{Price Change}} \times \text{Volume} / \text{Reserve} \\
&+ (2 \times \sqrt{\text{Price Change}} / (1 + \text{Price Change}) - 1.0) \times 100
\end{align*}
$$
where $\text{Fee Rate}$ is given as 0.3 in Sushiswap and $\text{Price Change}$ is defined as $\text{Price}_t / \text{Price}_{t-1}$.
Due to the shift (or lag) operator involved in the calculation, the `targets` start from 09/14/2020 whereas the `observables` start from 09/13/2020 for the `train` dataset.


## Benchmarks

Below shows the average performance for some benchmark models, aggregated from 10 different random seeds.
The performance was measured as the sum of Root-Mean-Square Error (RMSE) from the `targets` of each token pool.
The performance was measured for the testing period (11/01/2021 - 01/26/2022).


### Short-term Forecast - 1 Day

Model Name | ΣRMSE | Std
:--|:--:|:--:
Previous Day | 0.1846 | -
Moving Average (10 days) | 0.0843 | -
Random Forest | 0.1262 | 0.0062


### Long-term Forecast - 10 Days

Model Name | ΣRMSE | Std
:--|:--:|:--:
Previous Day | 0.1756 | -
Moving Average (10 days) | 0.1024 | -
Random Forest | 0.2420 | 0.0102
