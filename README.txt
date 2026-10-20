I.I.D. RENYI ENTROPY: VERIFIED UNIFORM MINIMAX THEOREM
====================================================

STATUS: THE FULL IID MINIMAX TARGET IS PROVED IN LEAN.

The capstone is Renyi.iid_renyi_full_verified : Renyi.FullManuscriptClaim,
in Renyi/FullIIDVerification.lean. Its proof has no certificate hypotheses.
The final build and both dependency audits pass; 4571 project theorem
declarations, including private/generated declarations, were audited.

STATEMENT AND MODEL

For every fixed accuracy 0 < epsilon < 1/2, there are positive constants
c_epsilon, C_epsilon and an alphabet threshold independent of alpha such
that, for every sufficiently large k and every real alpha > 1:

* some randomized estimator from at most C_epsilon * Renyi.rate iid
  samples estimates Renyi entropy within epsilon with failure at most 1/3;
* any randomized iid estimator achieving that accuracy and confidence uses
  at least c_epsilon * Renyi.rate samples.

The piecewise Renyi.rate is exactly the manuscript's regularized root rate
for noninteger orders below log(k), its integer extension, and k*log(k) at
high orders. The matching min-entropy endpoint is also proved.

The statistical model uses ordered iid observations on a labeled finite
alphabet and arbitrary randomized real-output estimators. The statements
are uniform in alpha and k. Orders may approach one or an integer, or grow
with k. Alpha = 1 is outside the manuscript's main theorem.

PRINCIPAL PROOFS

Renyi/FullIIDVerification.lean
  iid_renyi_full_verified and iid_renyi_uniform_minimax_verified.
Renyi/GeneralNonintegerIIDComplete.lean
  Complete general noninteger upper bound, with actual polynomial/Gamma
  statistic, random pilot, calibrated noise, and fixed iid implementation.
Renyi/NearOneIIDComplete.lean
  Complete upper bound uniformly for 1 < alpha <= 3/2.
Renyi/LowerComplete.lean
  Complete uniform iid lower bound for every real alpha > 1.
Renyi/EndpointLower.lean
  Matching integer, high-order, and min-entropy bounds.
Renyi/Model.lean
  The exact statistical definitions and target propositions.

REPRODUCING THE CHECK

Use Lean 4.24.0 and the bundled lake-manifest.json. Mathlib is pinned to
f897ebcf72cd16f89ab4577d0c826cd14afaafc7.

  lake exe cache get
  bash verify.sh

The library build treats warnings as errors. Audit.lean and KernelAudit.lean
each require the capstone to have type FullManuscriptClaim and check every
project theorem in the imported module closure, including private/generated
theorems. Both audits use the same Lean dependency collector; they are not
independent kernel implementations. Only propext, Classical.choice, and
Quot.sound are allowed.
There are no sorry/admit placeholders or custom axioms in the supplied
proofs. Python only generates audit queries and validates their output.

verification/theorem-inventory.json records the exact audited declarations,
module closure, and axioms. verification/source-hashes.json and provenance.json
record the delivered files. The build and audit logs are bundled.

SCOPE OF THE EXPOSITION INVENTORY

The main iid minimax statement and min-entropy endpoint are fully proved.
source-coverage.tsv separately inventories all 53 named exposition results.
Some supplementary identities and alternate derivations are still marked
PARTIAL; they are not assumed by the capstone proof. This archive does not
claim a proof of every separately displayed identity in the exposition.
In particular, the common-estimator identity across all orders and the
broader arbitrary-accuracy/arbitrary-confidence fixed-order specialization
are not fully formalized. The integer matching theorem is formalized for
0 < epsilon <= 1/2; the exposition states a wider accuracy range.

The archive omits toolchains, dependency copies, and compiled outputs.
The bundled readlink compatibility shim under verification/runtime concerns
this workspace runtime only; it does not modify Lean's proof checker and is
unnecessary on a normal installation.
