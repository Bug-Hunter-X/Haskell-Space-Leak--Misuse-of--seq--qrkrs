# Haskell Space Leak: Incorrect Use of `seq`

This repository demonstrates a common Haskell space leak caused by the misuse of the `seq` function.  The provided `bug.hs` file contains code that attempts to force evaluation of a potentially large data structure, but fails to do so completely due to an incomplete understanding of `seq`'s behavior.  The solution is shown in `bugSolution.hs`.

The primary issue is that `seq` forces only to weak head normal form (WHNF), not full evaluation. This can lead to substantial memory consumption if not handled carefully with larger data structures.  The solution provides a more robust approach to guarantee complete evaluation. 

**Key Concepts:**
* **Weak Head Normal Form (WHNF):** A value is in WHNF if its outermost constructor is known.  This isn't enough for complete evaluation of large structures.
* **Space Leaks:** Memory issues in Haskell that occur due to unevaluated thunks that aren't garbage collected because they're still referenced.