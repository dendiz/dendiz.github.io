---
{"dg-publish":true,"permalink":"/liquidate/","dg-note-properties":{"date":"2026-03-22"}}
---


Liquidate is a market simulation game, inspired by Wall Street
Raiders. It aims to provide an authentic and detailed simulation
of the economy and markets with the player buying/selling securities
to increase their net worth over time.

# Development Logs

## 2026-03-22
I have been mainly trying to understand how the markets function at a
macro level and how things are interconnected. It turns out (which
isn't really shocking)
that the markets are a global dynamic system (a.k.a mess on
interconnected things) where a change will create a ripple effect and
propagate through the system
until the system converges to a new state. Modelling this is best
approached with a stochastic process framework which I'm
investigating. My initial idea was to actually
have the whole market defined by this process but then I realized that
didn't lead to the granularity I'm after. I'm now exploring the
simulation of each participating corporation
in the market with it's own stochastic process to closely model the
alpha and beta for that entity.
