---
title: "Dissection: Market makers for Decred"
published_utc: 2019-08-22
updated_utc: 2019-08-22
---

_Updated 2019-08-22: removed unverified claim (see [Updates](#updates))_

This was a hard topic for me. As I realized later, for such big and important decisions there needs to be an [educational campaign](https://github.com/decred/dcrdocs/issues/971) before the proposals go live. I had to learn how it works, distill arguments, and reflect to build my own opinion.

First I've built an [index](https://github.com/decredcommunity/proposals/blob/master/market-makers/index.md) of all discussions about market maker proposals. Then I compiled [pros, cons, concerns and Q&A](https://github.com/decredcommunity/proposals/blob/master/market-makers/arguments.md) from different people. Finally, I wrote up my current view that you are reading now. The goal of this work was to clear up confusion surrounding market makers, come up with a vote choice for the RFP and prepare for judging the final proposals.

I may update this document but all changes will be visible via Git.

Apologies for the ton of bullets below. I separate statements and structure them in trees to see things better.

## Common misconceptions

- MM is for pump and dump
- MM will suppress the price
- MM will make huge profits on top of getting paid from Treasury
- MM and liquidity is for the (wealthy miniroty, the rich, whales, institutional investors) who need to easily enter and exit
- MM is just placing bags and is overpriced
- MM's prime goal is to increase trading volume
- MM's liquidity is inorganic
- MM is unethical
- MM should happen naturally
- MM must be provided by big holders

I am pretty sure all of these are misconceptions or at the very least one-sided, but am open for corrections.

Next I'll gradually build up the least controversial arguments I could come up with, plus some personal stuff.

## Words

First let's quickly define basic terms to make this easier for non-traders. If these are still difficult please read elsewhere:

- [limit order](https://www.investopedia.com/terms/l/limitorder.asp): order that hangs until someone fills it at your fixed price or until you cancel it
- bid: highest price someone is willing to pay (highest limit buy order)
- ask: lowest price someone is willing to sell at (lowest limit sell order)
- [market order](https://www.investopedia.com/terms/m/marketorder.asp): "instant" order, buy or sell at best available price (eat best bids/asks until you buy the desired amount)
- [slippage](https://www.investopedia.com/terms/s/slippage.asp): when the actual price of a trade differs from your expected price. Most commonly it means you sell cheaper than you want or buy higher than you want. Often it is a _loss_.
- [liquidity](https://en.wikipedia.org/wiki/Liquidity): limit buy and sell orders awaiting you any time, that allow you to _quickly_ buy or sell with _minimum slippage_. More liquidity is good for buyers and sellers.
- make: place limit order, _add_ liquidity
- take: place market order and immediately fill/consume limit orders, _remove_ liquidity
- [spread](https://www.investopedia.com/terms/s/spread.asp): the gap between bid and ask, difference between highest buy and lowest sell price. Smaller spread is more healthy
- market maker: one that sits on the market all day and facilitates trades between buyers and sellers
- [OTC](https://en.wikipedia.org/wiki/Over-the-counter_%28finance%29): "Over-the-counter", or simply off-exchange trading, is when two parties trade directly, often not disclosing their trade to the public, and often facilitated by a private OTC company

Market maker can make money in two ways:

1. By buying low and selling high, extracting value from the bid-ask spread. Bigger spread = more profit. In a way, such MM is getting paid by real buyers and sellers. Since all they wants is to profit from trading, such MM is not necessarily interested in high liquidity. _(perhaps they are not even called market makers and are just traders?)_
2. By getting paid by his customer to _provide liquidity_, minimize spread and serve better prices to real buyers and sellers. More liquidity provided = more profit. They aim to always _make_ liquidity but never _take_ it.

Market makers that we consider for hiring are type 2.

Apologies if the definitions are not precise since I'm not an expert. I tried to make it very simple. Corrections are welcome.

## 1. Market maker is doing useful work

Now let's get to what our MM does. There is a lot of confusion here.

- MM lets you _quickly_ convert small to medium amounts _without slippage_ (-> without losses)
- Without MM, if the market is thin as ours, you have a choice between two _pains_:
  - Spend time: place limit order at your desired price and wait. Still no guarantee it will get filled at that price if the price moves away. You _add_ liquidity and become the market maker yourself. Another possible time expense is finding an exchange that has enough liquidity for your trade and moving there
  - Take loss from slippage: buy or sell into other's limit orders and get less USD or DCR out of the trade. By the way, you _remove_ liquidity in this case. Another way to lose money is on fees to move your asset to a more liquid exchange
- MM serves as a bridge:
  - _in time_, by connecting today's sellers with tomorrow's buyers
  - _in space_, by connecting sellers and buyers on different exchanges _and_ OTC
- Success metrics for MMs are:
  - the bigger amount can be bought/sold without moving the price too much, the better
    - in other words, the lower slippage, the better
    - as a consequence, volatility is reduced in the small scale
  - the smaller the spread, the better
  - the higher uptime (% of time liquidity is present on the market), the better
  - increase in trading volume is desirable but is not the main goal
- Bonus: since MM monitors the market all the time they can provide useful insight for our researchers

An analogy I like is currency exchange service. Decent market maker is just as "inorganic" and "unethical" as a currency exchange office. Without it, you need to wait and/or actively find people willing to exchange your USD for EUR. Exchange office maintains buffers of both currencies and allows you to instantly convert from one to another at a stable price.

Market makers place new limit buy and sell orders but do not consume existing ones. In trading terms, they "make" orders, not "take" them.

## 2. Everybody benefits from better liquidity

Before discussing any particular MM choices I need to establish their desired properties.

Liquidity is thick and tight order books. The inability to move small and medium amounts in and out quickly hurts some legit use cases:

- Contractors need to spend time or take loss when they sell DCR to pay their bills
- People who buy and sell for DCR have poor experience with DCR as a medium of exchange
  - short term: merchants that accept DCR and sell it quickly may take a loss
  - long term: less confidence in being able to sell later
  - I do want DCR to be a good MoE
- Store of value properties suffer too
  - depending on how much time and loss it takes to "unfreeze" and use your value, you might look for more convenient alternatives
  - I want DCR to be a good SoV
- Investors have poor experience opening and closing positions
  - I will address them separately

Actually I lied, not everybody wins. MM smoothens the price curve. Traders who capitalize on big spreads and short term swings will lose profit.

The selling point of MM to "improve investors' experience" bugged me a lot so I had to dissect it. I narrowed it down to distaste for mere speculators, which triggered further thinking:

- Speculator-type "investors" buy and sell with profit as their number one goal, sometimes the only goal. They won't care about Decred's mission and principles, they will sell as soon as they smell fire (and they are good at it!), they won't endure hard times with us, and while they do hold DCR they will be bad stakeholders: they will either make bad decisions (because they don't care what Decred is about) or make profit-driven decisions. It's even worse if they are big.
- Many existing investors myself included somehow managed to get their DCR regardless of liquidity issues.
- If somebody has studied Decred but "poor liquidity" was the biggest factor that turned him off, it means other qualities of Decred were less important. To me they are _very_ likely a mere speculator. I may be wrong here, open to opinions.
- For the above reasons I don't want to onboard them or comfort them. I don't care if they are "institutional" or not. I don't actively hate them, just don't want to spend any resources on them.
- But I don't know how to filter them out without affecting everybody.
- Better liquidity helps all: those who care and those who don't.
- We should look for ways to collect the most intelligent and caring investors, but not by means of crippling _public_ infrastructure such as liquidity.
- For the "good" investors, I do want DCR to be easier to move in/out. They will waste less time and get a chance to contribute more.

Thinking about which investors I would like to join us made me revise all actors. At the cost of some repetition, another way to categorize legit use cases we want to help:

- we do want to better Decred as MoE for those who need to _exchange_ value
- we do want to better Decred as SoV for those who need to _store_ or _transfer_ value
- we don't mind to better Decred as investment for those who need to _increase_ value (on top of _storing_ it)

My personal mistake was to demand "high principles" from everybody. Upon a closer look I realized:

- In case of SoV and MoE, this is what Decred is being built for. It is looking to serve these groups regardless of their views.
- In case of investment, first, making people rich is not Decred's top priority. Second, I do have a preference about investor's principles. But it's hard to filter them and it should not come at the cost of everybody else.

With that cleared up, I realized that pitching market makers as a way to comfort "investors" who were blocked by liquidity is a wrong move. It paints an overall good idea (better liquidity for all) as a service to speculators, thus making MM less attractive and more confusing. And honestly, thinking about big players too much looks needy.

## 3. Why should the Treasury pay?

This question came up a lot.

I imagine 3 modes an entity trading on exchange can operate:

1. Manipulate price - pump, dump, or keep flat. The end goal is large scale profits or something else like attack a competitor/enemy or convince the public. I have no idea how it works but assume that good intelligence is key: you need to know how supply is distributed across exchanges, when can it move, how fast and and how much. The better intel and algorithms you have, the less money you can possibly burn.
2. Make money - extract profit from price moves. You want bigger spreads and bigger and more frequent price moves. Ideally you don't care about the price and can trade at any level.
3. Add liquidity to improve convenience for _others_. Unlike the other two, this is more likely to burn money than to earn. The gains are less direct.

I think a lot of people mix up these three and think MM is something evil or unethical. MM being considered is just as unethical or inorganic as your typical currency exchange service.

So our MM costs money and won't work for free. Who pays? Again, several options:

1. _Some_ stakeholders: far looking, aligned, coordinated and not too greedy ones. Let's say large holders and miners. Why would they? Because it is in "their own interest" and they believe good liquidity will strengthen their asset. Problems: a) this is uncertain and b) some will agree to pool funds while others will not ([tragedy of the commons](https://en.wikipedia.org/wiki/Tragedy_of_the_commons)). For each individual player it is a risk. Why would they risk their funds? Only if they can reap the reward. How will they extract it? Will they just hope for price increase, or trade and profit from the spread, or attempt a P&D?
2. _All_ stakeholders, via Treasury. Similar to a tax, it removes the "why should I pay when the other guy gets a free ride?" factor. Unlike tax, if you disagree with the majority the exit cost is low. Also, Decred's Treasury has been spending very carefully so far, so your effective tax is low.

Are these all options? In a fair system where it takes effort to obtain money, yes. But there is another source of funds:

3. Central entity that somehow obtained or printed a ton of money. Either by raising in an ICO, or by initial grab of a huge chunk of supply, or via ongoing founder rewards. This type can afford to throw lots of money at MM (and marketing).

Decred is type (2). Luckily it is not (3), and unfortunately, I believe (1) will not self-organize and perform as quick and efficient as (2), even in Decred.

A less mentioned potential strength of community-funded MM is that the community can insist on transparency and high quality public service over extraction of short term profits. For example, focus on tight spreads and low slippage, or support good exchanges regardless of their prestige (including DEX). If you pay for it, you control how to use the liquidity. This really depends on the standards of the community.

## 4. So what's next?

If we agree we want better liquidity, we agree (good) MM is doing useful work, and we consider hiring an MM, it boils down to the terms of the deal.

- I'd like to start as small as possible, build confidence and slowly scale up
  - $40K/month is a ton of money. Put in perspective, it is ~10% of monthly Treasury income and 15-20% of monthly spending (as of May-July 2019). It spends more than the team building our [novel DEX](https://proposals.decred.org/proposals/417607aaedff2942ff3701cdb4eff76637eca4ed7f7ba816e5c0bd2e971602e1) (and skilled developers is the biggest bottleneck in the space!). I want to be absolutely sure this money is doing a lot of good work
  - The freedom to scale MM down is limited by the level below which it either doesn't make much sense or is not interesting to the MM service provider
- If the minimum viable offer is still too expensive, shall we buy it now or wait for conditions to improve?
- Transparency is important: it will help to build confidence and provide intel for our next moves.

I don't have all the answers yet but I hope this has saved your time.

Feedback is welcome.

## Updates

* 2019-08-22: removed [reference](https://twitter.com/bettercio/status/1163340116120625152) to a $3.5M OTC purchase of DCR because apparently it was ["virtual"](https://twitter.com/BetterCio/status/1161170932318134272), i.e. imaginary. Very confusing, I may put it back upon clarification.
