# Detectability Collapse

A simulation report on how a strong signal spreading through a network becomes harder to detect as the network around it catches up.

**Live report and model:** https://seanman005.github.io/SPREAD-REPORT/

## The main idea

Detecting something unusual in a network depends on contrast: how much it stands out from everything around it. When a strong signal enters a network and spreads, it doesn't fade. The rest of the network rises to match it. Once everything looks the same, there's nothing left to stand out against.

So the signal becomes hard to detect not because it hides, but because the network evens out the difference that detection depends on.

## The model

- A network of **120 connected nodes**, built as a small-world network (Watts–Strogatz)
- A strong signal is injected at one or more entry points
- Each step, nodes can adopt the signal from neighbors. The bigger the difference between neighbors, the more likely it spreads
- Four measurements are tracked: how many nodes carry the signal, the network's average level, how much the strongest node stands out (detectability), and how traceable the entry points are

## Controls

| Parameter | What it changes |
|---|---|
| `grad` | How strong the injected signal is compared to the network |
| `cond` | How easily the signal passes between connected nodes |
| `ports` | Number of separate entry points (1–8) |
| `clust` | How tightly grouped the network is vs. how many long-range shortcuts it has |
| `cap` | How much more easily weaker nodes adopt the signal |
| `noise` | How unsettled the nodes are, which makes them adopt more readily |

## Key findings

1. **Spreading and becoming undetectable are two separate moments.** The signal covers most of the network first, and only later stops standing out. That gap, about 0.8–1.7 seconds across runs, is a window where the signal is everywhere *and* still detectable.
2. **Connection strength matters most.** `cond` controls the overall speed. Lowering it is the most reliable way to keep the signal detectable.
3. **Most other levers hit diminishing returns.** Past about 4 entry points or a noise level of 0.5, adding more barely changes anything.
4. **Detectability never reaches zero.** A small leftover contrast of about 3–5% always remains, located at the entry points.
5. **A surprise:** the fastest-spreading setup used a *less* tightly grouped network, because long-range shortcuts spread the signal faster than tight clusters do.

## Things to try

- Load **Optimized** and watch detectability drop as the network average rises to meet it
- Load **Slow** (low `cond`, 1 entry point). The signal stays visible the whole time and never fully spreads
- Set `ports` to 1, then 8, and compare how much contrast is left at the end
- Raise `noise` from 0 to 0.7 and notice it speeds things up but doesn't change the final contrast

## Limitations

- Each result comes from a single run, with no averaging, so small differences may just be randomness
- Traceability is calculated from a formula, not simulated, so that result is assumed rather than discovered
- `cap` was never varied, so that part of the theory is untested
- Detectability is measured with full knowledge of every node. A real detector would only see part of the network
- Only one network size (120 nodes) was tested

## Built with

JavaScript and HTML (model runs live in the browser). Result figures generated in Python with matplotlib.

## Author

Sean Obiacoro — Mechanical Engineering (Systems Emphasis), University of Utah, May 2027
