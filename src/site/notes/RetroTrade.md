---
{"dg-publish":true,"permalink":"/retro-trade/","dg-note-properties":{"date":"2026-02-01"}}
---


> RetroTrade is a back testing framework for trading strategies. 

The idea of a back testing is running your strategy
on historical data to see how it would have performed. RetroTrade does just that: Gives you a glimpse of what would
have happened. There are multiple intracracies to back testing ranging from hidden biases such as survivor ship bias
to look ahead bias that a back testing framework can never detect so the quality of any testing framework is highly
dependent on the data you feed it and the strategy implementation. 

RetroTrade supports the following operations

- Data ingestion
- Trading API
  - Partial orders
  - Slippage modeling
  - Commission modeling
  - Benchmark tracking

- Technical analysis API
- Stats API
- Performance reporting
  - Various risk/reward metrics
  - Portfolio performance reporting
  - Benchmarking
  - Transaction lists
  - Drawdown reports


Here is a screenshot of a report 


[![image](https://img.dendiz.xyz/images/2026/02/01/retrotrade-ss.html.md.png)](https://img.dendiz.xyz/image/EUQd)

# Development logs

### 2026-03-29

Major tasks tackled today were a refactoring of the modules to move stuff out of the mega exchange module into their own modules for better comprehensibility, new trading stats for win rate, average win vs average loss and expectancy (expected PNL based on win probability). 

While I was reviewing the code for the new report segment I noticed that the AI decided to compute this by consolidating the ledger of orders in a FIFO manner. This was actually interesting as I had unconsciously decided to use a ledger architecture feeling that it would be more flexible to just keep the history of things and consolidate when required so I took this opportunity to think a bit more deeply about the trade offs here. I think the major issue is that you need to compute everything on-demand but this is acceptable for the enormous flexibility this approach gives you. You could even run strategies where you are long and short the same asset in different strategies on the same simulation round. 

I think brokerages offer a kind of mixed model where you have multiple long positions possibly on different dates but as you close out the positions they are consolidated. E.g you have to choose which position you are closing out. In the end they should all amount to the same result in terms of equity curve but could have different tax implications due to the different taxation rules for different assets/positions etc. I'm not implementing any tax rules as I think that's out of scope and variable depending on where you live.


### 2026-03-28

Implemented trailing stops. This has been a long time waiting exit strategy that I can't wait to test. I've added a default percentage based trailing stop out of the box that will exit according to the min/max (depending on the direction of position) of the target price seen until the current tick. E.g if you set a trailing loss at 5% for a long position when the price is 100, and the price goes to 200 then 189 the position whil exit. I have left the strategy you pass on the trailing stop order flexible though as it is a protocol. So you could say have a ATRx3 or some other volatility based exit.

### 2026-03-27

Implemented with Gemini some long outstanding issues today. There was a half done migration to a new architecture to support more complex order types. Finished that transition and added support for limit orders and oco orders.

Transaction costs were also missing. Most US brokers seem to have dropped this but if you are using a platform in another country or trading crypto transaction costs still seem like an important factor for profitability computation.
