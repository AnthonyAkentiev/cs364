# cs364
CS364A: Algorithmic Game Theory (Stanford) by Tim Roughgarden

https://theory.stanford.edu/~tim/f13/f13.html

## Terms:

### Mechanism design

Mechanism design is a field in economics and game theory that takes an engineering approach to designing economic mechanisms or incentives, toward desired objectives, in strategic settings, where players act rationally. Because it starts at the end of the game, then goes backwards, it is also called reverse game theory. It has broad applications, from economics and politics (markets, auctions, voting procedures) to networked-systems (internet interdomain routing, sponsored search auctions).

### Strategic dominance
Strategic dominance (commonly called simply dominance) occurs when one strategy is better than another strategy for one player, no matter how that player's opponents may play. Many simple games can be solved using dominance. 
 
### Incentive-compatible
A mechanism is called incentive-compatible (IC) if every participant can achieve the best outcome to him/herself just by acting according to his/her true preferences.

### DSIC
The stronger degree is dominant-strategy incentive-compatibility (DSIC). It means that truth-telling is a weakly-dominant strategy, i.e you fare best or at least not worse by being truthful, regardless of what the others do. In a DSIC mechanism, strategic considerations cannot help any agent achieve better outcomes than the truth; hence, such mechanisms are also called strategyproof or truthful.

### BNIC
A weaker degree is Bayesian-Nash incentive-compatibility (BNIC). It means that there is a Bayesian Nash equilibrium in which all participants reveal their true preferences. I.e, if all the others act truthfully, then it is also best or at least not worse for you to be truthful

### Revelation principle

The **revelation principle** is a fundamental principle in mechanism design. It states that if a social choice function can be implemented by an arbitrary mechanism (i.e. if that mechanism has an equilibrium outcome that corresponds to the outcome of the social choice function), then the same function can be implemented by an incentive-compatible-direct-mechanism (i.e. in which players truthfully report type) with the same equilibrium outcome (payoffs)

# Lectures

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

### Revelation principle

The **revelation principle** is a fundamental principle in mechanism design. It states that if a social choice function can be implemented by an arbitrary mechanism (i.e. if that mechanism has an equilibrium outcome that corresponds to the outcome of the social choice function), then the same function can be implemented by an incentive-compatible-direct-mechanism (i.e. in which players truthfully report type) with the same equilibrium outcome (payoffs)

## Six - Simple Near-Optimal Auctions
Today we’ll seek out auctions that are simpler, more practical, and more robust than the theoretically optimal auction. Since optimality requires complexity, we can only hope that our auctions are approximately optimal. This is the second time we’ve turned to ap- proximation to escape a quandary posed by full optimality.

An interesting open research question is to understand how well the Vickrey auction with an anonymous reserve price (i.e., eBay) can approximate the optimal expected revenue in a single-item auction when bidders valuations are drawn from non-i.i.d. regular distributions. Partial results are known: there is such an auction that recovers at least 25% of the optimal revenue, and no such auction always recovers more than 50% of the optimal revenue.

The expected revenue of a Vickrey auction can obviously only be less than that of an optimal auction; yet the following result, due to Bulow and Klemperer, shows that this inequality reverses when the Vickrey auction’s environment is made slightly more competitive.

### Bulow-Klemperer theorem

The usual interpretation of the Bulow-Klemperer theorem, which also has anecdotal
support in practice, is that extra competition is more important than getting the auction format just right. That is, invest your resources into getting more serious participants, rather than sharpening your knowledge of their preferences (of course, do both if you can!).

A **Reserve Price** is a hidden minimum price that the seller is willing to accept for an item. 

The obvious experiment is to try out the theoretically optimal (and generally higher) reserve prices to see how they do. Yahoo!’s top brass wanted to be a little more conservative, though, and set the new reserve prices to be the average of the old ones ($.10) and the theoretically optimal ones.5 And the change worked: auction revenues went up several per cent (of a very large number). The new reserve prices were especially effective in markets that are valuable but “thin,” meaning not very competitive (less than 6 bidders). Better reserve prices were credited by Yahoo!’s president as the biggest reason for higher search revenue in Yahoo!’s third-quarter report in 2008.

Increasing the reserve price further does not have much effect on revenue.

## Seven - Multi-Parameter Mechanism Design and the VCG Mechanism

Theorem 2.1 (The Vickrey-Clarke-Groves (VCG) Mechanism) In every general mechanism design environment, there is a DSIC welfare-maximizing mechanism.

The upshot of the VCG mechanism is that, in general multi-parameter environments, DSIC welfare-maximization is always possible in principle. While it can be infeasible to implement in practice, the VCG mechanism nevertheless serves as a useful benchmark for other, more practical approaches.

Namely, the VCG mechanism can have bad revenue and incentive properties, despite being DSIC.

### Combinatorial auctions
A combinatorial auction has n bidders — for example, Verizon, AT & T, and several regional providers. There is a set M of m items, which are not identical — for example, a license awarding the right to broadcast on a certain frequency in a given geographic area.

For instance, suppose there are two bidders and two items, A and B. The first bidder only wants both items, so v1(AB) = 1 and is 0 otherwise. The second bidder only wants item A, so v2(AB) = v2(A) = 1 and is 0 otherwise. The revenue of the VCG mechanism is 1 in this example (exercise). But now suppose we add a third bidder who only wants item B, so v3(AB) = v3(B) = 1. The maximum welfare has jumped to 2, but the VCG revenue has dropped to 0 (exercise)! The fact that the VCG mechanism has zero revenue in seemingly competitive environments is a dealbreaker in practice. The revenue non-monotonicity in this example also implies numerous incentive problems, including vulnerability to collusion and false-name bids (see the exercises). None of these issues plague the single-item Vickrey auction.

## Eight - Combinatorial and Wireless Spectrum Auctions

Selling Items Separately.

There is a fundamental dichotomy between combinatorial auctions in which items are substitutes, and those in which items are complements — with the former being far easier, in theory and in practice, than the latter. 

In a spectrum auction context, two licenses for the same area with equal-sized frequency ranges are usually substitute items. Theory indicates that selling items separately has a chance to work well when items are (mostly) substitutes. 

With complements, welfare maximization (without incentive constraints) is already a very difficult problem; see also Problem 5. We cannot expect a simple auction format like separate single-item auctions to perform well in such environments.

### Simultaneous ascending auctions (SAAs)

Simultaneous ascending auctions (SAAs) form the basis of most spectrum auctions run over the last 20 years. We discuss the basic format first, and then some of the bells and whistles that have been added on over the years. Conceptually, SAAs are like a bunch of single-item English auctions being run in parallel in the same room, with one auctioneer per item. More precisely, each round, each bidder can place a new bid on any subset of items that it wants, subject to an activity rule. The activity rule forces all bidders to participate in the auction from the beginning and contribute to the price discovery discussed below. The details of an activity rule can be complex, but the gist is to require that the number of items that a bidder bids on only decreases over time as prices rise. Generally, the high bids and bidders are visible to all — even though this can encourage signaling and retaliatory bids (recall USWest vs. McLeod last lecture). The first round with no new bids ends the auction.

SAAs have two big vulnerabilities. The first problem is demand reduction, and this is relevant even when items are substitutes. Demand reduction occurs when a bidder asks for fewer items than it really wants, to lower competition and therefore the prices paid for the items that it gets.

The second big problem with SAAs, which is relevant when items are complements (in- cluding in many spectrum auctions), is the exposure problem. As an example, consider two bidders and two non-identical items. Bidder 1 only wants both items — they are comple- mentary items for the bidder — and its valuation is 100 for them (and 0 otherwise). Bidder 2 is willing to pay 75 for either item. The VCG mechanism would give both items to bidder 1, for a welfare of 100, and would generate revenue 75. In a SAA, though, bidder 2 will not drop out until the price of each item reaches 75. Bidder 1 is in a no-win situation: to get both items it would have to pay 150, more than its value. The scenario of winning only one item for a non-trivial price could be even worse. On the other hand, if bidder 2’s value for each item was only 40, then bidder 1 should just go for it. But how can bidder 1 know which scenario is closer to the truth? The exposure problem makes bidding in an SAA difficult for a bidder for whom items are complements, and it often leads to risk-averse, tentative bidding by such bidders.


