# cs364
CS364A: Algorithmic Game Theory (Stanford) by Tim Roughgarden

https://theory.stanford.edu/~tim/f13/f13.html

## One - Braess’s Paradox/Nash’s Theorem



## Two - Mechanism Design

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
1) strong incentive guarantees. It is dominant-strategy incentive-compatible (**DSIC**)
2) strong performance guarantees. If bidders report truthfully, then the auction maximizes the social surplus
3) computational efficiency. The auction can be implemented in polynomial (indeed,linear) time.

> What’s hard about mechanism design problems is that we have to jointly design two things: the choice of who wins what (allocation rule design), and the choice of who pays what (payment rule design).

#### DSIC (dominant-strategy incentive-compatible)

First, it is easy for a participant to figure out what to do in a DSIC mechanism: just play the obvious dominant strategy. Second, the designer can predict the mechanism’s outcome assuming only that participants play their dominant strategies, a relatively weak behavioral assumption.

### Three - Myerson’s Lemma

https://theory.stanford.edu/~tim/f13/l/l3.pdf

**Definition 4.1 (Implementable Allocation Rule)** An allocation rule x for a single-parameter environment is implementable if there is a payment rule p such the sealed-bid auction (x, p)
is DSIC.

**Definition 4.2 (Monotone Allocation Rule)** An allocation rule x for a single-parameter environment is monotone if for every bidder i and bids b−i by the other bidders, the alloca- tion xi(z,b−i) to i is nondecreasing in its bid z. 

That is, in a monotone allocation rule, bidding higher can only get you more stuff.

Awarding the good to the second-highest bidder is a non-
monotone allocation rule: if you’re the winner and raise your bid high enough, you lose. The reason is that raising your bid can only increase your position in the sorted order of bids, which can only net you a higher slot, which can only increase the click-through-rate of your slot.

**Theorem 4.3 (Myerson’s Lemma [2])** Fix a single-parameter environment.
1. An allocation rule x is implementable if and only if it is monotone.
2. If x is monotone, then there is a unique payment rule such that the sealed-bid mecha- nism (x, p) is DSIC [assuming the normalization that bi = 0 implies pi(b) = 0].
3. The payment rule in (b) is given by an explicit formula (see (6), below).

### Price formula (result)

![Formula 9](https://i.imgsafe.org/d0/d0bf7548c2.png)

Observe that the formula in (9) has the pleasing interpretation that, when its link its clicked, an advertiser pays a suitable convex combination of the lower bids.

### Generalized Second Price (GSP) is not DSIC
By historical accident, the sponsored search auctions used in real life are based on the “Generalized Second Price (GSP)” auction [1, 3], which is a simpler (and perhaps incorrectly implemented) version of the DSIC auction above. The per-click payment in GSP is simply the next lowest bid. Since Myerson’s Lemma implies that the payment rule in (9) is the unique one that yields the DSIC property, we can immediately conclude that the GSP auction is not DSIC. It still has a number of nice properties, however, and is “partially equivalent” to the DSIC auction in a precise sense. The Problems ask you to explore this equivalence in detail.

## Four - Algorithmic Mechanism Design

https://theory.stanford.edu/~tim/f13/l/l4.pdf

### Knapsack Auctions

When there is a shared resource with limited capacity, you have a Knapsack problem.

In a knapsack auction, each bidder i has a publicly known size wi (e.g., the duration of a TV ad) and a private valuation (e.g., a company’s willingness-to-pay for its ad being shown during the Super Bowl). The seller has a capacity W (e.g., the length of a commercial break). The feasible set X is defined as the 0-1 n-vectors (x1, . . . , xn) such that 􏰀ni=1 wixi ≤ W . (As usual, xi = 1 indicates that i is a winning bidder.) 

**Problem**: the alg. is NP-hard.

Check above the **desirable properties**:
1) DSIC
2) surplus-maximizing
3) Runs in polynomial time

The dominant paradigm in algorithmic mechanism design is to relax the second constraint (optimal surplus) as little as possible, subject to the first (DSIC) and third (polynomial-time) constraints.

### Non DSIC mechanisms

Can we do better than with DSIC mechanisms? The answer is “sometimes, yes.”

A very rough rule of thumb is that, for sufficiently simple problems like those in our introductory lectures, DSIC mechanisms can do anything non-DSIC mechanisms can. In more complex problems, like some discussed in the advanced lectures, weakening the DSIC constraint (e.g., to implementation in Bayes- Nash equilibrium) often allows you accomplish things that are provably impossible for DSIC mechanisms (assuming participants figure out and coordinate on the desired equilibrium). DSIC and non-DSIC mechanisms are incomparable in such settings — the former enjoy stronger incentive guarantees, the latter better performance guarantees. Which of these is more important will depend on the details of the application.

**Theorem 3.1 (Revelation Principle)** For every mechanism M in which every partici- pant has a dominant strategy (no matter what its private information), there is an equivalent direct-revelation DSIC mechanism M′.

The point of Theorem 3.1 is that, at least in principle, if you design a mechanism to have dominant strategies, then you might as well design for direct revelation (in auctions, truthful bidding) to be a dominant strategy.

Many equilibrium concepts other than dominant-strategy equilibria, such as *Bayes-Nash equilibria*, have their own Revelation Principle. Such principles state that, given the choice of incentive constraints, direct revelation is without loss of generality. Thus, truthfulness per se is not important; what makes mechanism design hard is the requirement that a desired outcome (without loss of generality, truthful reporting) in an equilibrium of some type. Varying the choice of equilibrium concept can lead to quite different mechanism design theories, with stronger equilibrium concepts (like dominant-strategy equilibria) requiring weaker behavioral assumptions but with narrower reach than weaker equilibrium concepts (like Bayes-Nash equilibria).
