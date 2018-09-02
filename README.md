# cs364
CS364A: Algorithmic Game Theory (Stanford) by Tim Roughgarden

https://theory.stanford.edu/~tim/f13/f13.html

## One

## Two

https://theory.stanford.edu/~tim/f13/l/l2.pdf

Each bidder *i* has a valuation *vi* — its maximum willingness-to-pay for the item being sold. 
Thus bidder *i* wants to acquire the item as cheaply as possible, provided the selling price is at most *vi*.

Our bidder utility model, called the quasilinear utility model, is as follows: 
If a bidder loses an auction, its utility is 0. If the bidder wins at a price *p*, then its utility is *vi* − *p*.

### Second-price (aka Vickrey) auction

A second-price or Vickrey auction is a sealed-bid auction in which the highest bidder wins and pays a price equal to the second-highest bid.

Second-price auctions are particularly easy to participate in — you don’t need to reason about the other bidders in any way (how many there are, what their valuations, whether or not they bid truthfully, etc.) to figure out how you should bid. Note this is completely different from a first-price auction. You should never bid your valuation in a first-price auction (that would guarantee zero utility), and the ideal amount to underbid depends on the bids of the other players.

The second important property is that a truthtelling bidder will never regret participating in a second-price auction.

In a second-price auction, every truthtelling bidder is guaranteed non-negative utility.

The Vickrey auction is awesome. Meaning, it enjoys three quite different and desirable properties:
1) strong incentive guarantees. It is dominant-strategy incentive-compatible (DSIC)
2) strong performance guarantees. If bidders report truthfully, then the auction maximizes the social surplus
3) computational efficiency. The auction can be implemented in polynomial (indeed,linear) time.

