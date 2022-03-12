# cairo-dutch
*Dutch Auctions implementation on StarkNet.*

## Overview
Dutch auctions are a way to conduct discrete sales of multiple homogeneous units of a good. Here is an implementation of Dutch Auctions that allows for a large sale of a token on StarkNet. Specifically, we enable the following behavior:
* A public read `price()` function that allows anyone to see the current price
* A public write `bid(num_tokens)` function that allows buyers to place an order for `num_tokens` of the base asset at the current price. It checks that the buyer has an adequate amount of the quote asset (e.g. USDC) to place the order, and if they do, then it transfers their token into the auction pool.
* A private read `locked_buying_power(address)` that allows an account owner to view their account value. In the initial version, we can make this publicly available.
* A public read `done()` function / boolean storage variable that reports True if the auction is done, and False otherwise.
* A public `allocate()` function that can be invoked by anyone in order to allocate the sale proceeds _and_ pay back all excess capital that was over-locked (does this by calling `locked_buying_power(address)` for each address).

## Milestones
[x] Set up dev environment / project skeleton with Nile.

[ ] Implement + briefly test token helper contract

    [ ] Figure out how to run and read/write to contracts locally to perform basic contract prodding.

    [ ] Find basic token contracts that allow incrementing of account value through public function call. Copy/paste into here, and make two tokens.

    [ ] Test out messing around with both tokens, increasing and decreasing token balance.
[ ] Implement + briefly test dutch auction contract

[ ] Implement token that can be bridged L1 <-> L2

    [ ] Implement an L1 contract that issues a wrapped token. This will be an ERC20 with the added functionality that our L2 contract is the only entity that can modify how much is owned by each account. This will be used to wrap the base and quote assets.

    [ ] Integrate the L2 Dutch auction contract to deposit / withdraw to/from the L1 contract.

    [ ] Integrate the L1 contract to withraw / deposit from/to the L2 contract.