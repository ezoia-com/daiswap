# Site

Visit https://www.daiswap.net. Both HTML and solidity code provided in this repository, so you can run your own too!

# Fees 

Swap contract takes a fixed 0.3% fee, fully passed on to liquidity providers. 

The swap with DAI is direct - only one fee is applied. 

Trading rates are bound between 0.95 and 1.05. You get a lot more liquidity in a smaller range, and will be less affected by front-running.

# Benefits for Poolers

Poolers get all of the fees, without taking on the risks of an intermediary pair (e.g. you need to fund DAI/ETH and USDC/ETH for Uniswap). 

By taking advantage of the limited spread of stablecoin swaps and compressing the trading range, a larger proportion of deposited tokens can take part in the swap, and you are likely to benefit from more fees. 

# Swap Design Goals 

The swap contract uses the constant product model popularised by Uniswap, but adds a twist, by simulating the presence of a much larger pool of tokens. 

This restricts the exchange rate to a much tigher range, which is more useful for like-for-like swaps. (e.g. WETH/ETH, or Stablecoin/Stablecoin). 

The simulation works by a baseMultiplier factor, currently set to 40, which adds (baseMultiplier * totaldai) to both token counts of the constant product multiplier. 

The swap contract is written with minimal onchain logic, configurability and state, instead leveraging off both the underlying ERC20 tokens, with their addresses hardcoded into the contract. 

This makes it easier to reason the correctness of the swap contract, but any undiscovered issues in the underlying contracts may break expected behaviour. 

With sufficient liquidity (e.g. if 5 to 10% of the entire DAI pool were deposited), this can act as a data point for MakerDAO's stability fee feedback. 

Other stablecoin-pairings can also be easily launched: PAX, TUSD, USDT, GUSD. 

Once other pairings are deployed, a separate simple and state-less swapping contract can be built and deployed, allowing easy Stablecoin-Stablecoin swaps through the DAI pairing. 

# Automated Smart Contract Analysis 

Securify - https://securify.chainsecurity.com/report/21ff7cc391e2653ed6887969477658d6c97dbedc313310613baadca671a173ef
Smartcheck - https://tool.smartdec.net/scan/8a202883e77b482c807dd74695c546b0

# Token details

Contract address (Source verified by Etherscan) - 0x236cce40a3e83313c03bc29e5f693bfd1d6e9034 

ABI

[{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"daiposit","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"dai","type":"uint256"}],"name":"swapForUSDC","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"dai","type":"uint256"}],"name":"calcSwapForUSDC","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"withdraw","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"dai","type":"uint256"}],"name":"sharesFromDai","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"shares","type":"uint256"}],"name":"usdcAmountFromShares","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"dai","type":"uint256"}],"name":"deposit","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"totaldai","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"usdc","type":"uint256"}],"name":"calcSwapForDai","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"dai","type":"uint256"}],"name":"usdcAmountFromDai","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"usdc","type":"uint256"}],"name":"swapForDai","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"baseMultiplier","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"}

# Collaboration
Please feel free to copy, fork, redesign, debug, or anything, really. I can be reached at hello@ezoia.com if you like to discuss anything! 
