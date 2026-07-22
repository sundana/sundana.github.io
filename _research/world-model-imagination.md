---
title: "When World-Model Imagination Hurts: A Controlled Diagnostic in Lightweight Model-Based RL"
status: ongoing
desc: Diagnosing why imagined rollouts destabilize lightweight MBRL. Controlled encoder-matched experiments show multi-step latent drift corrupts returns; horizon truncation to h=1 restores stability.
---

Model-based reinforcement learning (MBRL) often attributes sample-efficiency gains to imagined rollouts, but these gains can be confounded by larger model capacity rather than by imagination per se. We study lightweight MBRL under matched parameter budgets on a MiniGrid credit-assignment ladder and add a same-encoder control that toggles imagination on/off while keeping representation capacity and online world-model training fixed.

Across two credit-assignment tasks, model-free PPO is consistently more stable under matched budgets, while unrestricted imagined rollouts introduce mid-training collapse that widens with task horizon. Same-encoder controls reveal that $DoorKey-5x5$ imag-OFF is perfectly stable ($15/15$ clean sustain) against $4/15$ imag-ON, and on $Empty-16x16$ the corresponding ratio is $11/15$ vs. $0/15$.

Diagnostics show that the world model is one-step accurate (5&ndash;7&times; better than persistence), yet its multi-step autoregressive latent rollouts drift monotonically to the inter-step latent scale within the imagination horizon, corrupting imagined returns. Ablations confirm that horizon truncation to <em>h=1</em> substantially improves stability (clean sustain $3/5$, final-5 $0.96$), whereas lower synthetic-data mix ratios and drift-based gating provide limited or inconsistent recovery, indicating that lightweight imagination remains fragile unless rollout length is tightly controlled.

<p>On exploration-bottlenecked tasks, both methods are limited by stochastic reward discovery, establishing the credit-assignment regime as a necessary precondition for any imagination benefit. Our results bound the operating regime where lightweight imagination is unsafe and identify horizon-limited or representation-auxiliary use of small world models as safer than unrestricted multi-step imagination in lightweight MBRL.</p>
