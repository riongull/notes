# Dash Unit Denomination - Problems & Solution

##### About this document
This document presents the problems with Dash's unit denomination convention.  It also presents potential solutions to these problems, along with the foreseeable challenges the community faces in fixing the system.

### Overview



### Background
We've had these discussions before in bitcoin, a good solution never really emerged (it was too late)

##### past discussions

###### bitcoin
* [Reddit discussion]()
* [Reddit discussion]()
* [Reddit discussion]()
* [bitcointalk discussion]()
* [article]()
* [article]()

###### dash
* [Forum discussion]()
* [article]()

### Problems

##### psychological
* people think dash is (will be) "expensive"
* people think they own little after they've paid much

##### technical
* existing software is tailored to 100 subunits per unit

##### practical
* visually, it's difficult to keep track of where the decimal is
  * some people write `.0123`, some people write `0.1234`
* verbally, it's harder to say "123 thousandths of a dash" than "123 thousand dash"

### Solution
The solutinon is to re-denominate the units.  This is merely a shift in nomenclature (naming convention).  
* We are *not* suggesting expanding the money supply
* We are *not* doing this to pump the price

##### re-denomination
`1 dash` --> `1,000,000 dash`
* what we now call `1 dash` (equal to `100,000,000 duffs`), will henceforth be identified as `1,000,000 dash` (but still equal to `100,000,000 duffs`)

##### key benefits
* works with existing software

##### key costs
A lot of software will need to be updated.  It's better now than later.  Some upgrades may need to be funded by the treasury, particularly major 3rd party integrations such as ATMs and exchanges (Poloniex, etc).  Foreseeable software updates include:  
* core software updates
* peripheral software updates
* exchange software updates (may need to fund)
* documentation updates
* wallet and software

### Before and After

##### present values
|                       Price |  Present Convention | Proposed Convention | Comment                                                                              |
|----------------------------:|:-------------------:|:-------------------:|--------------------------------------------------------------------------------------|
| Present money supply (DUFF) | 700,000,000,000,000 | 700,000,000,000,000 | Amount of duffs do not change                                                        |
| Present money supply (DASH) |      7,000,000      |  7,000,000,000,000  | What we now call 1 DASH will be 1,000,000 DASH after the change                      |
|    Denomination (DASH/DUFF) |     100,000,000     |         100         | Each DASH will be subdivided into 100 DUFF instead of 100,000,000 DUFF               |
|            Price (USD/DASH) |         $12         |      $0.000012      | Today's prices (present and proposed convention)                                     |
|            Price (JPY/DASH) |        ¥1200        |        ¥0.012       | Japan is already in the 4-digit pricing (when USD catches up it will look like this) |
|            Value (DASH/USD) |   0.08333333 DASH   |    83,333.33 DASH   | 1 USD buys you `x` DASH (at present and proposed conventions)                        |
|            Value (DASH/JPY) |   0.00083333 DASH   |     833.33 DASH     | 1 JPY buys you `x` DASH (at present and proposed conventions)                        |


### Freeform Remarks
*


### Summary
