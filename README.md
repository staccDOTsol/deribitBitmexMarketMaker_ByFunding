# Hey!

## I cannot and will not assure or imply returns. Risk only what you can afford to lose.

## Telegram: https://t.me/ManyVolumeSignalMonster

# Performance

https://i.imgur.com/E7qB0nW.png

# How To Use

0. I noticed I had dozens of clones and dozens of re-clones from my GitHub repository, while only a few people used the referral code.
1. Email me at jarettrsdunn+git@gmail.com with video proof or screenshots of BitMEX/Deribit new account creation (verification emails) from today, using below links.
2. I'll confirm my affiliate counter has gone up by 1.
3. I'll then either add you to the private repository or send you a .zip of the files.
4. Thanks!


## Sign Up Here


https://www.bitmex.com/register/EJy18M (note to self: +bmex) EDIT: bitmex now working with current version in bitmex2.py!


https://www.deribit.com/reg-4393.9303


## NOTE!


Neither Mex nor Deribit care how many accounts you have. You can only verify once, but you can have as many unverified accounts as you like. Please, if you already have a mex or deribit account, do sign up for another one with the above links. It helps the cause and the positive energy is felt for days, rest assured :) :D



## Summary


I ran a modified version of my market making bot for a day or two. 


The new strategy, in testing.py, as you may be aware, was to long and short perps and futures based on funding +/-.


Here's where the bot was after 7-8 hours. https://i.imgur.com/HFf6rxr.png


44% gains ain't nothin' to laugh at!


Afterwards, it took a bit of a dive, then eventually liquidated out as BTC grew $$ hundreds in ~1hr. https://i.imgur.com/6jMtbYs.png


The good news here is that the strategy works. There are risk factors that were too generous in this run, specifically the % of balance to have entered into long/short positions. 


there's 2 options


1. more balance, in which case 44% becomes 4.4%
2. lower pct lims, in which case 44 becomes maybe 44 maybe 20 maybe 14 but definitely not 4.44, and it wouldn't get wiped out
3. Add SL/TP


## BTC or BTC/ETH or ETH


The bot on testing.py is built on BTC+ETH balance, and will fail without it.


To run just BTC, change the def get_futures line from:


i[ 'instrumentName' ]: i for i in insts  if ('BTC-' in i['instrumentName'] or 'ETH-' in i['instrumentName'] )  and i[ 'kind' ] == 'future'#  


to:


i[ 'instrumentName' ]: i for i in insts  if ('BTC-' in i['instrumentName'] )  and i[ 'kind' ] == 'future'#  


or to run just ETH:


i[ 'instrumentName' ]: i for i in insts  if ('ETH-' in i['instrumentName'] )  and i[ 'kind' ] == 'future'#  



After serious consideration, I've added SL/TP to testing.py on Deribit!


## Settings


In bitmex-settings and deribit-settings are arrays.


Directional
0. none
1. StochRSI


Price
0. best bid/offer
1. vwap
2. BitMex Index Difference
3. BBands %B


Volatility
0. none
1. ewma
2. BBands Width
3. ATR


Quantity
0. none
1. BitMex Index Difference
2. PPO
3. Relative Volume
4. BBands %B


hey mate! You'll want to open up testing.py and enter in your KEY and SECRET. You'll want to then scroll down and find pct_lim_long and short, which will be more or less if you want more or less exposure. Next, pct qty base is your entry order # - you'll want to make it a multiple of what it is set to now then by % of your balance relevant to $500 (so if you have $1k, double it). Next, risk_charge_vol is what base amount to have between your order layers on the books - increase it to trade less often. Next, TP and SL should be much less if you want it to exit when position reaches that % ROI on your deribit interface. It's a decimal value, so TP SL of 0.25 would be 25% ROI +/- to exit. Now, in your terminal/console run pip install deribit_api ccxt requests pandas finta quantstats, then run python testing.py. When you run it, if all is well, you should see it enter futures at $10 and perpetual at $40 a whole bunch of times.


If you're running BTC and ETH can you do me a favor..


find these lines:


if 'PERPETUAL' in fut:
pos_lim_short = pos_lim_short * (len(self.futures) - 1)
pos_lim_long = pos_lim_long * (len(self.futures) - 1)


change them to:


if 'PERPETUAL' in fut:
pos_lim_short = pos_lim_short * (len(self.futures) - 1) / 2
pos_lim_long = pos_lim_long * (len(self.futures) - 1) / 2



find the two lines that say:



qty = qty * len(self.futures)



change them to:



qty = qty * len(self.futures) / 2

# A Recent Email

loads of changes. significant change is that it market orders 1/10 of the amount if pos >350 <-350, every interval, and adjusts the 1/10 mark to achieve a consistent 75% maker volume.


This lessens the overall risk and allows for a higher pos_lim_long & short.


The more we can keep delta neutral, the less we have to worry about significant moves.


How's the bot been running for you? Are you my ref also running eth?


We might also want to kill march futures (by default on btc on repo, just remove 'btc-' from 'btc-mar20' and it'll also kill eth mar fut) because we're close to expiry.


SLs now reduce to delta neutral, instead of marketing out the entire position. This is extremely helpful in not losing a whole bunch of $ on SL, meaning we can SL more often.


Moon!

# A Recent Reddit Post

Market Maker UP 7.5% before September futures fundnng flipped sides: https://i.imgur.com/gKM1zkU.png


Up a whole 240% at all-time high, settling around 130-140% after September futures dropped below perpetual price, realizing gains on convergence of cash n carry futures arbitrage: https://i.imgur.com/mAEKnJE.png


What is it?


This Deribit and BitMEX market making bot earns on fee rebates when making an individual post-only limit order turn into a position. It also gains from the (average) difference in spread on an individual instrument, and as I saw overnight while I was sleeping it gains significantly on the convergence of perp vs futures arbitrage based on funding rates.

Moon!


You can review the bot's graph in real-time here: http://jare.cloud:8080 - note that since the huge climb and for most of today it took a break, as it noticed the increase in balance and decided to sleep for a day (the higher of my two Takeprofit values). I've manually intervened and it's now pumping out trades again.


I'm offering the bot FREE of charge for those people who use my referral link. My referral link earns a % of fees when people market out of a postiion (every other ordering cycle it reduces it's skew, and on either layer of stoploss/takeprofit it first reduces it's skew back to delta-neutral then all the way down to 0 position). I believe in Free and Open Source as a religion - and while the final bot that we end up putting into production will have configs and values fed to it by our AI at Coindex Labs, the Intellectual Property for the bot without AI is mine and I decide to share it. There would need to be literally tens of millions of dollars on this bot for it to hurt anyone else's edge.


While I'm asking for people to sign up for referral links, I've closed the repository with the bot until after people provide proof they've signed up on the referral link. While the bot was 100% open-source before, I noticed that 40 people cloned the repository in one day while I only received maybe 2 referral link signups - which isn't sustainable. Once you sign up on the referral link, you're free to review the code in full or have someone audit it.


You need to enter your key and secret to the testing.py file for Deribit or bitmex2.py file for BitMEX for the bot to function. It never ever sends these keys anywhere other than to the exchanges, and when it's sent to the exchange it's hashed into a signature that people can't figure out. Moreover, on an exchange like Deribit so long as the keys aren't withdraw keys then there's very little risk in using them in the first place.

Moon!

https://github.com/DunnCreativeSS/deribitBitmexMarketMaker_ByFunding

# Some Recent Setup Instructions

the defaults are live on jare.cloud:8080


you'll want to enter key into testing.py for deribit


there's directions on the repo


you'll need to pip install a few packages


along with python first


well


you'll want to adjust pct_qty_base down or up if you want smaller or larger order sizes


max_skew down or up if you want the max exposure +/- to be down or up


pct_lim_long and pct_lim_short down or up if you want the total position in a given direction to be less or more


risk_charge_vol smaller or larger if you want the distance between orders and best bid/offer to decrease/increase


also, in the current version


you'll want 2 deribit accounts


one has about 1/5 the balance it's key and secret, the main accoutn is key2 and secret2


it'll hold a short for the amount of $USD you hold in the first account


that's where the 100% came from -  the shorts


the idea is 1. there will be convergence of futures arbitrage


2. if btc declines, you want to hedge against that so you don't lose too much USD$


In times of high volatility, if you want it to trade more often change RISK_CHARGE_VOL to 1/2 or 1/3 what it is now


and if it takes a break for 1hr too often (it'll tell you in the console) find this line:

if self.vols[k] > 3:

change it to:

if self.vols[k] > 5.5:
