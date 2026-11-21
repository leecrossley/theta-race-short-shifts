# How fast can a split–inert prime race move?

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24410822.svg)](https://doi.org/10.5281/zenodo.24410822)

This result is now maintained in [theta-host-split-inert-race](https://github.com/leecrossley/theta-host-split-inert-race/tree/main/results/theta-race-short-shifts). This repository is archived and keeps its releases and DOI.

On the 547/727 theta-lift host, the normalized lead can rise or fall by more than **1.9735 times the logarithmic distance moved**. This happens arbitrarily far out, for every fixed window width and every fixed move up to a doubling. The same bound holds for the instantaneous logarithmic slope and for averages over widths and moves.

Let $K=\mathbf Q(\zeta_{16}+\zeta_{16}^{-1})$, $F=K(\sqrt{397669})$ and $E=K(\sqrt{-547},\sqrt{-727})$, where $397669=547\cdot727$. Count prime ideals of the degree-eight field $F$. For each prime $v$, write $\epsilon(v)=1$ for split and $-1$ for inert in $E/F$. At a good prime, the product of normalized first-step theta trace jumps above $v$ equals $\epsilon(v)$. The concrete admissible datum and the degrees of both fields are checked in Lean. [Field and character frame](SecondField.lean) · [Trace identity](RaceTrace.lean)

## The bound

For $b>1$ give a prime of norm $n$ the weight $\log n\thinspace W_b(n/y)$, where

$$
W_b(t)=
\begin{cases}
 b(1-1/t),&1 < t\le b,\\
 b^2/t-1,&b < t < b^2,\\
 0,&\text{otherwise}.
\end{cases}
$$

Write $A_b(y)$ for the weighted inert count minus the weighted split count. Set $B_b=2\sqrt b(\sqrt b-1)^2$ and $S_b(y)=A_b(y)/(B_b\sqrt y)$. For every fixed $b>1$ and $1<r\le2$,

$$
\liminf_{y\to\infty}\frac{S_b(ry)-S_b(y)}{\log r}<-1.9735,
\qquad
\limsup_{y\to\infty}\frac{S_b(ry)-S_b(y)}{\log r}>1.9735 .
$$

For example, the lead gains more than $1.9735\log(1.01)$ and loses more than that amount at arbitrarily large locations only one percent apart within each pair. The two directions can occur at different locations. The score itself also has $\liminf S_b<-5.6921$ and $\limsup S_b>7.6921$.

The full theorem permits any fixed compactly supported probability distribution of widths and moves with the windows aligned at their geometric centres. It includes a move of zero logarithmic length by taking the derivative. The bounds hold for the resulting average and require neither GRH nor an independence conjecture. [Theorem and proof](PROOF.md)

## Where the numbers come from

Five certified zero ordinates of the relevant Dirichlet factors lie near $0.04853636$, $0.24857218$, $0.43421666$, $0.44601153$ and $0.57961560$. Two computations checked the five crossings and all 928 exclusions for signed combinations. A separate interval cover verified the real segment for all eight factors. Differencing two windows cancels the contribution of prime squares. Each selected zero still contributes with the same phase throughout the allowed range of moves. That gives the quantitative bound even after averaging. [Numerical checks](evidence/check.txt) · [Lean proof of the multiplier bound](ShiftBound.lean)

For $b=r=2$, a direct count gives a normalized slope between $-12.294$ and $-12.293$ from $y=25$ to $50$, then between $34.499$ and $34.500$ from $50$ to $100$. This count omits the rational ramification primes $2,547,727$. Deleting any fixed finite set leaves the asymptotic bounds intact. [Prime-ideal enumeration](independent.py)

The earlier 571/599 result bounds the height of a lead. This result also controls its change across a prescribed distance, including the limiting derivative. The compact kernel and the finite-frequency oscillation method have earlier sources. [Prior-work comparison](PRIOR-WORK.md)

## Reproduce the checks

Python 3 with `python-flint==0.9.0` runs the three arithmetic checks.

```sh
python3 -m venv .venv
. .venv/bin/activate
python -m pip install -r requirements.txt
python verify.py
python independent.py
python real_axis.py
```

For the full replay on x86-64 Linux, install Git, curl, tar, zstd and a C toolchain, activate the Python environment above, and run `bash verify-release.sh`. The script checks the manifest, fetches the pinned sources, replays the Lean modules and compares the output with the published receipt. A prebuilt Mathlib environment and source cache can be used on another supported platform. [Replay commands and trust boundary](PROOF.md#replay) · [File hashes](SHA256SUMS)
