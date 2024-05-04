# BESS - 101

## Forward Prices

There are several methodologies to generate forward prices used in the valuation of supply; these methodologies may be combined for better resolution of the final output - an hourly (or sub-hourly) price curve that extends out 25 years.

### Forward Prices - Energy Markets

Three commonly deployed ways to determine the future price of a market are using production cost modeling, employing stochastic processes, and generating futures prices.

#### Production Cost Modeling

Production cost modeling describes the expected value at a node at a future date. It is dependent on the topology of the generating units described in the model and does not account for the path between right now and the value at delivery, which could be an hour from now or 25 years from now. Production cost modeling is a useful exercise because it can account for changes in the supply stack and demand. This methodology is often employed by consulting companies like Aurora, ICF, and nFront. One consequence of this approach is that the described future price may be incongruent to the value that the market ascribes to it today and can result in a significant disconnect when hedging one or more components of risk.

#### Stochastic Process

A stochastic process based approach assumes prices move with a mix of drift and random changes. Generating a futures curve requires a description of constraints, upper and lower limits, as well as temporal relationships between hours, days, and months, and even years. A base curve reflects the expected outcome and is a probability weighted blend of multiple scenarios. The multiple scenarios generated also lend themselves to accessing a low and high case. The important assumption in this process is that the feedstock is historical data and that these curves most often reflect the expected value at a future date, not the value of the future date today. The output of this approach shares commonalities with a PCM based approach and offers the same strengths and weaknesses.

#### Market-based Approach

The third approach is a market based approach which relies on historical data, observable information from traded markets - like ICE Cleared Futures and CRRs - and calculates a forward curve that reflects the value at every interval today instead of the expected value at the future date. Every desk that manages risk in the marketplace employs this approach to “mark” curves every day and track the risk and value of the portfolio. This approach is congruent to the traded exchange and otc markets and allows for the most efficient transfer of risk and de-risking.

BatteryOS is unique in marking energy curves at over 50,000 bus bars across 6 ISOs in North America. The ability to generate a forward curve at any location instantly allows BatteryOS to forecast revenue at any location instantly, which in turn allows BatteryOS to assess the standalone and relative value of any location instantly.

### Forward Prices - Ancillary Services

Modeling forward prices is non-trivial. Modeling ancillary services prices is more complex. Load, supply from variable generation (like wind and solar), a relationship with energy prices all combine to produce a meaningfully accurate view on forward ancillary service prices. The relation between energy and ancillary service prices is not one to one, but the quality of the output is directly linked to the quality of the forward energy price.
