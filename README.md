# yearn-data

Last updated on 01/26/2022.

All data is crawled from the Ethereum Mainnet.


## lp-strategies

Customized toy dataset from Sushiswap data for the performance evaluation of various statistical models. Please see the separate [README file](lp-strategies/) for more information.


## sushiswap

On-chain data for the pairs listed in Sushiswap.
Data was crawled from [one of the subgraphs on The Graph](https://thegraph.com/hosted-service/subgraph/zippoxer/sushiswap-subgraph-fork), following the [awesome work from reednaaxeelaa](https://github.com/reednaaxeelaa/AMMroi)(https://amm.vav.me).

File names within the directory follow the pattern of `[token0]&[token1].csv`.

Column Name | Data Type | Description
:--|:--|:--
datetime | datetime (UTC) | Datetime when the block was created
liquidityProviderCount | int
reserve0 | float
reserve1 | float
reserveETH | float
reserveUSD | float
token0Price | float
token1Price | float
totalSupply | float
trackedReserveETH | float
txCount | int
volumeToken0 | float
volumeToken1 | float
volumeUSD | float


## uniswapv2

On-chain data for the pairs listed in Uniswap V2.
Data was crawled from the [hosted service on The Graph](https://thegraph.com/hosted-service/subgraph/uniswap/uniswap-v2).

File names within the directory follow the pattern of `[token0]&[token1].csv`.

Column Name | Data Type | Description
:--|:--|:--
datetime | datetime (UTC) | Datetime when the block was created
liquidityProviderCount | int
reserve0 | float
reserve1 | float
reserveETH | float
reserveUSD | float
token0Price | float
token1Price | float
totalSupply | float
trackedReserveETH | float
txCount | int
volumeToken0 | float
volumeToken1 | float
volumeUSD | float


## yearn_strats_daily

On-chain data for the strategies deployed/revoked in the V2 Vaults at Yearn.
Data was crawled using a local version of the wonderful [yearn-exporter](https://github.com/yearn/yearn-exporter).

Column Name | Data Type | Description
:--|:--|:--
timestamp | datetime (UTC) | Datetime when the block was created
vault | string
strategy | string
activation | timestamp \| int
lastReport | timestamp \| int
totalDebt | float
totalLoss | float
totalGain | float
estimatedTotalAssets | float
