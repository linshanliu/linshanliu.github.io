---
title: "Arbitrage-Free Volatility Surface"
excerpt: "A C++ pipeline that extracts implied volatilities from option prices, fits an SVI smile per maturity, and checks the fitted surface for arbitrage."
collection: portfolio
---

Market option prices don't imply a single volatility -- they imply a whole curved surface across strikes and maturities, the "volatility smile." Fitting that surface is a standard task in quant finance, but a curve that fits the market points well can still be financially nonsensical: it can imply a negative probability, which is arbitrage -- a theoretical money machine that shouldn't exist.

This project builds the full pipeline, from raw option prices to a validated surface: inverting Black-Scholes prices into implied volatilities (Newton-Raphson), fitting each maturity's smile with the industry-standard SVI parameterization via a from-scratch Nelder-Mead optimizer, and then explicitly checking each fitted curve against the Durrleman no-arbitrage condition -- reporting not just whether a slice fails, but exactly where.

The most interesting design decision was choosing SVI specifically because its derivatives are available analytically, letting the arbitrage check use exact math instead of numerically differentiating a noisy fitted curve twice (a second numerical derivative on market noise is a well-known way to get garbage). The output is a per-maturity diagnostic table: fit quality and arbitrage status, side by side.

Below is the actual implied-volatility surface fitted from the project's sample option chain -- drag to rotate, scroll to zoom.

<div style="border-radius:12px;overflow:hidden;border:1px solid #222;">
<iframe src="/files/spcx_vol_surface.html" style="width:100%;height:520px;border:none;display:block;"></iframe>
</div>
[Code and full technical writeup &rarr;](https://github.com/yourusername/your-repo-name)
