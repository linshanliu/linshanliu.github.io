---
title: "Finite-Difference PDE Option Pricer"
excerpt: "A C++ solver that prices options by numerically solving the Black-Scholes PDE, with theta-scheme time-stepping (explicit / Crank-Nicolson / fully implicit) unified in one class.<br/><img src='/images/pde-pricer-thumb.png'>"
collection: portfolio
---

Most option-pricing tutorials stop at the Black-Scholes formula. But the formula only exists for the simplest contracts — add a barrier, or let volatility depend on the stock price, and the closed form disappears. This project builds the numerical machinery that survives that jump: instead of solving for a price directly, it solves the *equation* the price obeys, on a discretized grid, marching backwards from the option's expiry to today.

The core design choice was to make the same code path handle three very different numerical behaviors — explicit, Crank-Nicolson, and fully implicit time-stepping — through a single continuous parameter (θ), rather than three separate implementations. This matters because each scheme trades off speed, accuracy, and stability differently, and switching between them (e.g. a few implicit steps to smooth a payoff's sharp corner, then switching to the more accurate Crank-Nicolson) becomes a one-line change instead of a rewrite.

The architecture separates the PDE, the payoff, the boundary conditions, and the grid into independent, swappable pieces — so extending the solver to barrier options or local volatility later doesn't require touching the core engine. Every result is validated against the closed-form Black-Scholes formula as an independent check.

[Code and full technical writeup →](https://github.com/yourusername/your-repo-name)
