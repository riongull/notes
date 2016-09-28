# Dash Unit Denomination - the Problem & the Solution

### Overview
Dash prices are problematic.  If they aren't fixed now, the problem will get worse, and it will soon be practcally impossible to fix.  The problem is Dash's unit denomination convention.  This document explains the problem and presents the solution.  The solution will be costly, but it will provide many benefits.

### Background
The problems Dash faces are not new in cryptocurrency, The bitcoin community has had these discussions before.  It has been, and continues to be, a lengthy debate, and to this point no good solution has emerged.  This is because bitcoin didn't see these problems ahead of time.  It may be too late for bitcoin to fix the problem, but dash can fix the problme before it gets too late.

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

### The Problem
The problem is that the generally-used unit of account in the dash ecosystem is too large.  The unit we call `DASH` (comparable to `USD`, `EUR`, `JPY`, etc) represents too much *value*.  The manifestation of the problem is that items purchased, denominated in `DASH` are very small, fractional amounts of a `DASH`.  The problem is much more appraent in everyday, small purchases such as the proverbial cup of coffee.  Already it costs a fraction of a `DASH` to purchase a cup of coffee.  With increased consumer adoption, this problem will get much, much worse, to the point where almost anything someone buys will cost a fraction of one unit of account.  People are not accustomed to thinking in fractional values.   

##### psychological
* People (will) think dash is *"expensive"*
* People feel they *own relatively little dash* after they've paid relatively much in their currency (e.g. dollars)

##### technical
* Existing software is tailored to *100 subunits per unit*

##### practical
* It's difficult to grasp conceptually how much you are paying when you see a dash price  
* It's difficult to see where the decimal is, and it's inconsistent from person to person
  * some people write `.0123`, some people write `0.1234`
* It's harder to say "123 thousandths of a dash" than "123 thousand dash"

### The Solution
The solutinon is to **re-denominate the units**.  This is merely a shift in *nomenclature* (naming convention).  
* We are *not* suggesting expanding the money supply
* We are *not* doing this to pump the price

##### re-denomination
* `1 DASH` --> `1,000,000 DASH`
  * What we now call `1 DASH` (equal to `100,000,000 DUFF`), will henceforth be identified as `1,000,000 DASH` (which will still be equal to `100,000,000 DUFF`)


##### key benefits
* Working with whole numbers is better than decimal units
* We don't need to come up with new complex naming conventions as price increases
* It will be more compatible with existing financial software
* People will be more cognizant of purchasing power increases over time
  * Last month this coffee cost me 2,000 DASH, now that same coffee costs only 1,300 DASH

##### key costs
A lot of software will need to be updated.  It's better now than later.  Some upgrades may need to be funded by the treasury, particularly major 3rd party integrations such as ATMs and exchanges (Poloniex, etc).  Foreseeable software updates include:  
* Core software updates
* Peripheral software updates
* Exchange software updates (may need to fund)
* Documentation updates
* Wallet and software

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
* We're going to have to tackle this proplem sooner or later
* All of the solutions bitcoin came up with were sub-optimal, and there still isn't consensus
