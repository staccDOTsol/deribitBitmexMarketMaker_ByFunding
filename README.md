# Hey!

# Performance

https://i.imgur.com/E7qB0nW.png

# How To Use

0. I noticed I had dozens of clones and dozens of re-clones from my GitHub repository, while only a few people used the referral code.
1. Email me at jarettrsdunn+git@gmail.com with video proof or screenshots of BitMEX/Deribit new account creation from today, using below links.
2. I'll confirm my affiliate coutner has gone up by 1.
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


hey mate! You'll want to open up testing.py and enter in your KEY and SECRET. You'll want to then scroll down and find pct_lim_long and short, which will be more or less if you want more or less exposure. Next, pct qty base is your entry order # - you'll want to make it a multiple of what it is set to now then by % of your balance relevant to $500 (so if you have $1k, double it). Next, risk_charge_vol is what base amount to have between your order layers on the books - increase it to trade less often. Next, TP and SL should be much less if you want it to exit when position reaches that % ROI on your deribit interface. It's a decimal value, so TP SL of 0.25 would be 25% ROI +/- to exit. Now, in your terminal/console run pip install deribit_api ccxt requests pandas finta, then run python testing.py. When you run it, if all is well, you should see it enter futures at $10 and perpetual at $40 a whole bunch of times.


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


