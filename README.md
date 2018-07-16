# Contextual Equivalence for a Language with Continuous Random Variables and Recursion

Coq development of theorems and proofs for the paper: "Contextual Equivalence
for a Language with Continuous Random Variables and Recursion" by Mitchell
Wand, Ryan Culpepper, Theophilos Giannakopoulos, and Andrew Cobb (ICFP 2018,
https://doi.org/10.1145/3236782).

Requirements:

- Coq 8.6 (also tested with Coq 8.8)
- [Autosubst](https://github.com/uds-psl/autosubst) (use the `coq86-devel` branch)
- [Coquelicot](http://coquelicot.saclay.inria.fr/)


# Getting Started

On a fresh Ubuntu 18.04 system, the following steps are sufficient to
install Coq and the libraries that our code depends on.

- install coq and coquelicot via opam:
  - `sudo apt install build-essential git opam m4`
  - `opam init --auto-setup`
  - ```eval `opam config env` ```
  - `opam repo add coq-released http://coq.inria.fr/opam/released`
  - `opam install coq.8.8.0 coq-coquelicot.3.0.2`
     - Note: this step might fail on machines with less than 3 GB memory.
     - This also installs `coq-mathcomp-ssreflect.1.7.0`, a dependency
       of Coquelicot.
- check out, build, and install autosubst:
  - `git clone -b coq86-devel https://github.com/uds-psl/autosubst.git`
    - The head commit of branch coq86-devel was d0d7355797.
  - `pushd autosubst`
  - `make`
    - This may print warnings: "fix/cofix without a name are deprecated...".
      These warnings may be ignored.
  - `make install`
  - `popd`
- compile our coq development:
  - `make`


# Overview

We have formalized the development of the small-step semantics, measure
semantics, logical relation, CIU relation, contextual ordering, and entropy
shuffling. For the most part, the proofs directly follow the proofs in the
paper. We have not formalized the big-step semantics or the applications of
the CIU relation to prove specific equivalences.

We use the Autosubst library to manage binders in the syntax and the
Coquelicot library for representing and reasoning about real numbers. In
addition to the axioms provided by the Coquelicot library, we also have
axiomatized the entropy source and basic properties of Lebesgue integration,
such as linearity and monotonicity, Lebesgue's monotone convergence theorem,
and Tonelli's theorem, for integration with respect to the measure on the
entropy source. We have also taken functional extensionality and restricted
forms of the law of the excluded middle as axioms.


# File layout

- `Basics.v`: Non-domain specific tactics and hints for auto.
- `Measures.v`: Axioms about measure theory and lemmas about measure theory and
  real analysis. Also axiomatizes the entropy space (Section 2.2).
- `Syntax.v`: The syntax and static semantics of programs and related
  lemmas (Section 2.1).
- `OpSem.v`: The small-step operational semantics for execution using
  a single entropy (Section 2.3.1).
- `MeasSem.v`: The measure semantics (Section 2.4). We do not
  formalize the measurability of functions, so this does not include
  Lemma 2.13.
- `LogRel.v`: The definition of the logical relation (Section 3).
- `Compatibility.v`: The compatibility lemmas and the fundamental theorem for
  the logical relation (Lemma 3.1 and Theorem 3.2).
- `CIU.v`: The definition of the CIU `CIU` relation and the proof of equivalence
  with the E relation `Erel` (Section 4).
- `CTX.v`: Direct and indirect definitions of contextual ordering, the proof of
  the equivalence of those relations, and the proof of equivalence with `Erel`
  and `CIU` (Section 5).
- `Interpolation.v`: The interpolation and genericity theorems for manipulating
  small-step semantics as if they were big-step semantics (Theorems 2.8 and 2.9).
- `EntropyShuffling.v`: Lemmas about Entropy reshufflings that preserve
  measure (Section 6.2).


# Acknowledgment

This material is based upon work sponsored by the Air Force Research Laboratory
(AFRL) and the Defense Advanced Research Projects Agency (DARPA) under Contract
No. FA8750-14-C-0002. The views expressed are those of the authors and do not
reflect the official policy or position of the Department of Defense or the
U.S. Government.
