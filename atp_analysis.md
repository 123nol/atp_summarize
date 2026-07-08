# Concept Analysis: *Automated Theorem Proving*
### Frank Pfenning, Carnegie Mellon University (Draft of Spring 2004)

> A note on the source: this is a 144-page set of graduate course notes (CMU's "Automated Theorem Proving," taught 1997–2004). The author's own preface asks that the document not be cited or distributed, as it is a rough draft. What follows is my own analysis and explanation of the material for your personal study, in my own words — not a reproduction of the text.

The book is a single sustained argument: start from the *meaning* of the logical connectives (natural deduction), and derive, in a principled and provable way, one increasingly refined proof-search procedure after another — sequent calculus, focused derivations, the inverse method, labeled deduction, and equality reasoning — each justified by soundness/completeness theorems with respect to the last. Almost everything in the book is instrumental to that one throughline, so the concept map below is organized exactly as the book's own chapters, since that *is* the logical dependency structure.

---

## Part 1 — Full Concept Outline

**1. Introduction**
- Judgment vs. proposition; historical lineage (Frege → Russell → Hilbert → Gentzen → Martin-Löf)
- Backward-directed vs. forward-directed proof search
- Why intuitionistic logic is the chosen vehicle
- The course's build-a-prover-incrementally project structure

**2. Natural Deduction**
- 2.0 Judgments: categorical, hypothetical, parametric; derivations as evidence
- 2.0 Alternative ways to found a logic: Hilbert axiomatization / combinatory logic; categorical logic; Gentzen's natural deduction
- 2.1 Intuitionistic Natural Deduction
  - Terms and propositions grammar
  - The judgment "A true"; structural properties (hypothesis, weakening, duplication, exchange)
  - Introduction/elimination rule methodology; orthogonality of connectives
  - Local soundness (reduction) and local completeness (expansion)
  - Rules connective-by-connective: ∧, ⊃, ∨, ¬ (via a parametric judgment), ⊤, ⊥, ∀, ∃
- 2.2 Classical Logic
  - Three equivalent extra rules: proof by contradiction, double negation, excluded middle
  - Multiple-conclusion alternative
- 2.3 Localizing Hypotheses
  - Contexts Γ; the judgment Γ ⊢ A
  - Structural properties as *theorems*, proved by induction, instead of built-in assumptions
  - Analytic vs. synthetic judgments (Martin-Löf)
- 2.4 Proof Terms
  - Curry–Howard isomorphism; propositions-as-types, proofs-as-programs
  - λ-calculus term assignment per connective; β-reduction / η-expansion as computation

**3. Sequent Calculus**
- 3.1 Intercalation
  - Normal-deduction search strategy (introductions bottom-up, eliminations top-down)
  - The ⇑ / ↓ judgments and the coercion between them
  - Soundness of normal deductions; the difficulty of completeness; annotated deductions with an extra coercion rule as a bridge
- 3.2 Compact Proof Terms
  - Removing redundant type annotations via bidirectional type-checking (synthesizing vs. checking terms)
- 3.3 Sequent Calculus proper
  - Turning eliminations "upside down" into left rules; introductions into right rules
  - Sequents Γ ⇒ A; initial sequents; per-connective left/right rules
  - Soundness/completeness with respect to natural deduction
  - The cut rule and sequent calculus *with* cut
- 3.4 Cut Elimination
  - Admissible vs. derivable rules
  - Gentzen's Hauptsatz; nested induction (on the cut formula, then on the derivations)
  - Cut elimination theorem
- 3.5 Applications of Cut Elimination
  - Confluence and strong normalization remarks
  - Normalization theorem for natural deduction (as a corollary chain)
  - Consistency; the disjunction and existential properties; independence of excluded middle
- 3.6 Proof Terms for Sequent Derivations
- 3.7 Classical Sequent Calculus
  - Splitting truth into "A true" / "A false" / contradiction
  - Rule of contradiction; excluded middle as a *derived* judgmental principle, not an axiom
  - Three notations for the same judgment (Γ # Δ, Gentzen's Γ ⇒ Δ, signed A⊤/A⊥)
  - New classical connectives ⇒ and ∼ (since intuitionistic ⊃/¬ cannot be given classical left/right rules without losing their meaning)
  - Kolmogorov's double-negation translation into intuitionistic logic, and its inverse
- 3.8 Exercises

**4. Focused Derivations**
- 4.1 Inversion
  - Invertible vs. non-invertible rules; "don't-care" vs. "don't-know" non-determinism
  - Synchronous vs. asynchronous propositions
  - The four-zone sequent Δ; Ω ⇒ A; · / Δ; Ω ⇒ ·; R
  - Soundness/completeness of inversion proofs; termination of the asynchronous phase
- 4.2 Backchaining
  - Horn clauses/goals/theories; the "uniform proof" search discipline
  - Compiling a Horn theory into inference rules; connection to forward chaining / unit resolution
  - Open problem: combining forward and backward strategies
- 4.3 Focusing
  - Generalizing backchaining to full intuitionistic logic
  - Four focusing judgments; focus / blur rules
  - Connections to Andreoli's linear-logic focusing, Herbelin's LJT, Huang's assertion-level proofs
- 4.4 Unification
  - Existential non-determinism and meta-variables
  - Residuation: enriching sequents with a residual "unification-logic" formula
  - The unification algorithm as constraint transformation; occurs-check
  - Termination and satisfiability-preservation theorems
- 4.5 Unification with Parameters
  - The dependency problem (∀x∃y vs. ∃y∀x); Skolemization vs. explicit parameter-dependency tracking
  - Pruning; the restriction judgment t |∆
- 4.6 Exercises

**5. The Inverse Method**
- Forward vs. backward search reconsidered: monotonic knowledge growth, no disjunctive non-determinism, but large conjunctive non-determinism
- 5.1 Forward Sequent Calculus
  - Reinterpreting Γ → C as "all of Γ is needed"; loss of weakening; assumptions as sets
- 5.2 Negation and Empty Succedents
  - Gentzen's empty-right-hand-side device, avoiding propositional parameters
- 5.3 The Subformula Property
  - Signed (positive/negative) subformulas; the Signed Subformula Property theorem
  - The resulting forward-search procedure
- 5.4 Naming Subformulas
  - Labeling compound subformulas to avoid repeated scanning
- 5.5 Forward Subsumption
  - The subsumption order on sequents; propositional decision procedure; backward subsumption
- 5.6 Proof Terms for the Inverse Method
- 5.7 Forward Sequent Calculus for First-Order Logic
  - Extended subformula/immediate-subformula relation; schematic variables vs. parameters
- 5.8 Factoring
  - Incompleteness without post-hoc contraction after unification; the factoring rule
- 5.9 Inverse Focusing
  - Combining focusing with the inverse method; "stable sequents"; deriving problem-specific inference rules
- 5.10 Exercises

**6. Labeled Deduction**
- Relativized truth, "A true at world p"; motivation (fully invertible sequent calculus)
- 6.1 Multiple Conclusions
  - The judgment Γ ⇒ᵐ Δ; why naive rules break intuitionistic soundness; the corrected ⊃R rule
- 6.2 Propositional Labeled Deduction
  - Labels as sequences of parameters; scope-as-label-extension
  - Monotone sequents; the Completeness of Labeled Deduction theorem
- 6.3 First-Order Labeled Deduction
  - Labeled terms; labeled parameter contexts
- 6.4 Matrix Methods
  - Connection/mating methods unifying both labels and terms

**7. Equality**
- 7.1 Natural Deduction for Equality
  - Reflexivity as introduction; two "replace s by t" / "replace t by s" elimination rules
  - Why the second elimination rule is *derivable* but still indispensable for normalization
  - Proof terms: `refl`, `subst₁`, `subst₂`; bidirectional typing
- 7.2 Sequent Calculus for Equality
  - Why naive left rules for equality break cut admissibility
  - The fix: restrict equality rules to atomic formulas, applied last; separate "equational" from "regular" derivations
  - Admissibility of cut with equality (four-part theorem)

---

## Part 2 — Detailed Elaboration

### 1. Introduction

The book opens by situating automated deduction historically: Frege's *Begriffsschrift* as the first attempt at a formal reasoning language, undone by Russell's paradox; Russell and Whitehead's type-theoretic repair in *Principia Mathematica*; Hilbert's simpler predicate calculus; and finally Gentzen's *natural deduction*, which explains each connective by the inference rules that introduce and eliminate it. This is presented as the decisive methodological choice for the whole book: meaning-via-inference-rules is more modular and more amenable to proof than an axiomatic presentation, because each connective can be studied (and later, extended or removed) independently of the others.

A second organizing idea introduced here is the split between **backward-directed** proof search (working from the goal toward the axioms — tableaux, connection/matrix methods, resolution) and **forward-directed** search (working from the axioms toward the goal — classical resolution, the inverse method). The book studies both, and one of its throughlines is that most search strategies used in real theorem provers can be *derived from* the sequent calculus rather than invented independently.

Finally, the choice of **intuitionistic logic** as the logic of study is justified on three grounds: its Curry–Howard correspondence to typed functional programs (of central interest to programming-languages research); its greater structural complexity relative to classical logic, which exposes phenomena classical logic's special symmetries hide; and the existence of a clean embedding of classical logic inside it (studied later, in §3.7), which lets classical reasoning be studied *through* the intuitionistic machinery.

### 2. Natural Deduction

**Judgments.** The foundational move is to treat *judgment* (an act of asserting something, on the basis of evidence) as prior to *proposition*. Two judgment forms recur throughout the book: a **hypothetical judgment**, "J₂ under hypothesis J₁," evidenced by a derivation of J₂ that may use J₁ freely (zero or more times, in any order); and a **parametric judgment**, "J for any a," evidenced by a derivation that is uniform in an arbitrary parameter a. These two notions — hypothetical and parametric reasoning — are treated as more primitive than any particular logic, and every logic in the book is built by instantiating them.

The main judgment of natural deduction is "A true." Contrasting this with other ways of founding a logic is instructive: a **Hilbert-style axiomatization** uses only "A true" with no hypothetical judgments, which forces heavy reliance on the implication connective inside axioms (and, when proof structure is made explicit, yields combinatory logic); **categorical logic** instead takes entailment ("A entails B") as basic. Gentzen's natural deduction, by contrast, freely uses both hypothetical and parametric judgments, which is what allows every connective to be defined in total isolation from the others — a property the book calls **orthogonality**, and treats as essential for later modular extensions (adding equality, quantifiers, new connectives, etc. without disturbing what's already proved).

**Introduction/elimination methodology.** For each connective, an **introduction rule** states the minimal circumstances under which a compound proposition may be concluded true, and an **elimination rule** states what may be deduced from the truth of that compound proposition. Two meta-properties keep these rules honest:
- **Local soundness**: introducing a connective and immediately eliminating it should be reducible to a strictly more direct derivation not using the connective at all (an elimination rule that fails this is "too strong" — it lets you conclude more than the premises warrant).
- **Local completeness**: eliminating a connective should retain enough information to reconstruct it via the introduction rule (an elimination rule failing this is "too weak").

These are witnessed, respectively, by **local reduction** rules (a detour-removal transformation, essentially a computation step) and **local expansion** rules (an "eta"-style unfolding). This is the calculus's built-in self-check: every connective's rules must pass both tests before they're accepted as meaningful.

**Per-connective rules.** Conjunction, implication, and the quantifiers follow a very natural pattern (pairing/projections for ∧; hypothetical discharge/modus ponens for ⊃; new-parameter introduction/instantiation for ∀ and ∃). Disjunction is the first place a subtlety appears: the elimination rule cannot simply extract "A true" from "A ∨ B true" (that would make the system inconsistent — from one theorem you could derive everything), so instead the elimination rule requires a **proof by cases**, discharging two hypothetical sub-derivations at once. **Negation** is treated in a self-contained way (rather than defining ¬A as an abbreviation for A ⊃ ⊥) by using a judgment parametric in an arbitrary proposition p: if any p follows from assuming A, then ¬A holds. **⊤** has only an introduction rule (no information to extract, hence no elimination rule); **⊥** has only an elimination rule (nothing should ever justify introducing it, but once assumed, anything follows) — the book notes the helpful heuristic of seeing ⊤ as a "0-ary conjunction" and ⊥ as a "0-ary disjunction," which explains the missing rules as the vacuous case of the pattern used for ∧/∨.

**Classical logic (§2.2).** Ordinary intuitionistic natural deduction cannot derive propositions like A ∨ ¬A. Classical logic is obtained by adding *one* of three equivalent extra rules — proof by contradiction, double-negation elimination, or excluded middle — each of which breaks the tidy introduction/elimination pattern (they don't correspond to any single connective). The book flags this as evidence that natural deduction is, at heart, an intuitionistic calculus, and that classical symmetries are much better exhibited in a sequent-calculus setting (developed later in §3.7).

**Localizing hypotheses (§2.3).** Up to this point, "correct use of a hypothesis" was a *global* property of an entire derivation (tracked implicitly by matching discharge labels). This section makes it *local* by explicitly carrying a context Γ (a list of labeled hypotheses) in every judgment, turning "A true" into "Γ ⊢ A." The four structural properties that were previously silent background assumptions — exchange, weakening, contraction (the ability to reuse or discard hypotheses freely, in any order) — become *theorems*, each proved by straightforward structural induction on derivations. This section also introduces the substitution theorem (if Γ,u:A ⊢ C and Γ ⊢ A then Γ ⊢ C), the operation that underlies both cut-elimination later and ordinary β-reduction. The chapter closes by noting, following Martin-Löf, that once hypotheses (and later, proof terms) are fully localized, the truth judgment becomes *analytic* rather than *synthetic* — it carries its own evidence rather than requiring an appeal outside itself.

**Proof terms (§2.4).** The **Curry–Howard isomorphism** is introduced: propositional natural-deduction derivations correspond exactly to simply-typed λ-calculus terms, with propositions playing the role of types. Each connective's rules get a term-level reading: ∧ becomes pairing/projection, ⊃ becomes λ-abstraction/application, ∨ becomes tagged injections plus a case construct, ⊥ becomes `abort`. Local reduction becomes ordinary β-reduction (substituting an argument term into a function body); local expansion becomes η-expansion. This section is where the reader sees, very concretely, that proof normalization *is* program evaluation — the correspondence that later grounds "propositions as types, proofs as programs."

### 3. Sequent Calculus

**Motivating the sequent calculus (§3.1, Intercalation).** The chapter's opening problem is to make precise a very natural proof-search heuristic: apply introduction rules working backward from the goal, and elimination rules working forward from the hypotheses, hoping the two directions "meet in the middle." This is formalized with two new judgments — A ⇑ ("A has a normal deduction") and A ↓ ("A is extracted from a hypothesis") — built by restricting each natural-deduction rule according to whether it's an introduction (bottom-up, produces ⇑) or an elimination (top-down, consumes and produces ↓), plus one **coercion** rule that lets an extraction stand in as a normal proof where needed. Soundness of this restricted system (it only proves what natural deduction proves) is easy. Completeness is not: naively translating an arbitrary natural deduction into this bidirectional format can hit a "conflict" where an elimination immediately follows an introduction and the classification breaks. The book's fix is to *temporarily* re-admit the missing coercion (from normal *to* extraction) as an extra rule, prove the resulting "annotated" system sound and complete with respect to ordinary natural deduction (straightforward, by induction), and only later (§3.4–3.5) prove that this extra coercion was never actually needed — which is precisely the content of cut elimination.

**Compact proof terms (§3.2)** observes that once derivations are classified as normal/extraction, the corresponding proof terms carry redundant type annotations (e.g. on every λ-abstraction). The fix is **bidirectional type-checking**: split terms into those whose type is *synthesized* (elimination terms — variables, applications, projections) and those *checked* against an expected type (introduction terms — pairs, abstractions, injections), which exactly mirrors the ⇑/↓ split above. This is proved to give a decidable, unambiguous type-checking procedure (Theorem 3.4).

**The sequent calculus itself (§3.3)** is obtained by literally "flipping eliminations upside down" into so-called **left rules** (operating on a proposition assumed as a hypothesis) while introductions become **right rules** (operating on the goal). The basic judgment "A left"/"A right" is packaged into a **sequent** Γ ⇒ A, where propositions on the left may include not just original hypotheses but anything derivable from them by elimination, and the proposition on the right is exactly what natural deduction would call the conclusion. Each connective gets a left and a right rule built mechanically from this recipe; **initial sequents** Γ, A ⇒ A correspond to the earlier ⇑/↓ coercion, *not* to ordinary hypothesis use. The chapter proves soundness (Γ ⇒ A implies Γ ⊢ A ⇑) directly by induction, and proves completeness with respect to normal deductions using a substitution lemma for extractions plus weakening/contraction lemmas. To connect the sequent calculus to *arbitrary* (not just normal) natural deductions, the book adds the **cut rule** —

> from Γ ⇒ A and Γ, A ⇒ C, conclude Γ ⇒ C

— read as "prove a lemma A, then use it." Soundness/completeness of "sequent calculus with cut" against the annotated natural-deduction system of §3.1 is then straightforward, setting up the central theorem of the next section.

**Cut elimination (§3.4)** is the book's centerpiece. The key conceptual distinction drawn first is between an **admissible** rule (one that happens to preserve derivability in the current system, but might not survive if new connectives are added) and a **derivable** rule (one with a direct proof from the existing rules, hence robust under any extension). Cut turns out to be *admissible but not derivable* — a subtlety worth noting, since it means every time the logic is extended (e.g. with equality, in Chapter 7) the admissibility argument has to be redone, not merely inherited.

The proof of **admissibility of cut** (Theorem 3.11) — "if Γ ⇒ A and Γ, A ⇒ C then Γ ⇒ C" — is a **nested induction**: an outer induction on the structure of the *cut formula* A, and an inner induction on the structure of the two given derivations. The case analysis is organized around whether the cut formula A is the *principal formula* (the formula the last inference rule is "about") of the final step in either derivation:
- If A isn't principal in either, the cut can simply be pushed one step upward past whichever inference doesn't concern A.
- If A *is* principal on both sides simultaneously — e.g. the left derivation ends by introducing A ∧ B on the right, and the right derivation ends by eliminating A ∧ B on the left — the two matching rules "annihilate" into a smaller cut (or two smaller cuts) on the immediate subformulas, which is exactly why the induction on the cut formula's *size* is what makes the whole argument terminate.

From this, **cut elimination proper** (Theorem 3.12) follows almost for free: any derivation using cut can be rewritten, one cut at a time, into a cut-free derivation, by repeatedly invoking admissibility.

**Applications of cut elimination (§3.5)** are where the theorem earns its keep. Because the *construction* in the admissibility proof is non-deterministic (several cases can apply to the same derivation), different eliminations of the same cuts can, in principle, yield different final derivations — the book notes this is resolved by a **confluence** property (up to so-called *commutative conversions*) that has to be established separately, while **termination** of any run of the algorithm falls directly out of the induction already used to prove admissibility (**strong normalization**). Chaining together all of §3.1–§3.4's soundness/completeness theorems yields the **Normalization Theorem for Natural Deduction**: every derivable proposition has a *normal* natural deduction. From cut-free provability, several deep structural facts follow almost by inspection of which sequent-calculus rules could possibly conclude a given sequent (a technique called **inversion**):
- **Consistency**: `⊢ ⊥` is not derivable, because no cut-free rule concludes the empty-hypothesis sequent `· ⇒ ⊥`.
- **The disjunction property** (if `⊢ A ∨ B` then `⊢ A` or `⊢ B`) and the **existential property** (if `⊢ ∃x.A` then `⊢ [t/x]A` for some term t) — both hallmarks of a constructive logic, unavailable in classical logic.
- **Independence of excluded middle**: there is no general derivation of `⊢ A ∨ ¬A` — again by direct inversion, since the only route to `¬A` fails at the required "new parameter" side-condition.

**Classical sequent calculus (§3.7)** revisits classical logic, but now starting from the sequent calculus rather than natural deduction, because Gentzen's classical sequent calculus retains a strong **subformula property** that natural deduction's ad hoc extra rule (§2.2) lacked. The judgment is re-split into three primitives: `A true`, a new `A false` (usable only as an assumption), and a judgment of outright **contradiction** (`contr`). A single **rule of contradiction** (a proposition cannot be simultaneously true and false) turns out to be strong enough that the **principle of excluded middle** becomes a *provable meta-theoretic principle* rather than a primitive inference rule — a striking result, since it means classical reasoning's most controversial law is, in this framing, forced by the very structure of the true/false judgments rather than assumed outright. Three equivalent notations for this "true-and-false" judgment are compared: the book's own `Γ # Δ`, Gentzen's classical **multiple-conclusion** sequent `Γ ⇒ Δ`, and a "signed formula" notation (`A⊤`, `A⊥`). A key discovery here is that ∧ and ∨ behave identically in classical and intuitionistic logic — the *only* connectives that genuinely differ are implication and negation, which is why the classical calculus introduces brand-new connectives `⇒` (classical implication) and `∼` (classical negation) rather than reusing `⊃`/`¬`. Finally, **Kolmogorov's double-negation translation** is developed in full: a map `(·)ᵒ` embedding classical propositions into intuitionistic ones (inserting `¬¬` in front of most connectives) such that classical derivability corresponds exactly to intuitionistic derivability of the translated sequent — one precise sense in which "classical logic is a fragment of intuitionistic logic," proved via a companion "backward" translation `(·)ᵉ` and a round-trip equivalence lemma.

### 4. Focused Derivations

**Inversion (§4.1)** attacks the practical problem left open by the raw sequent calculus: proof search still has to *guess* which rule to apply and in what order, and most of those guesses don't matter. The key distinction is between **invertible** rules (whose premises are derivable exactly when the conclusion is — applying them can never lose completeness, so their order is irrelevant, i.e., "don't-care non-determinism") and **non-invertible** rules (where the choice genuinely matters and might need backtracking — "don't-know non-determinism"). A precise **Inversion Theorem** lists exactly which rules are invertible (e.g. `∧` on the right, `⊃` on the right, `∀` on the right, `∧`/`∨`/`∃`/`⊤` on the left) versus not (e.g. `∨`/`∃` on the right, `⊃`/`∀` on the left), each non-invertibility witnessed by an explicit counterexample sequent. This licenses classifying every connective as **asynchronous** (decomposed eagerly, in any order, with no backtracking) or **synchronous** (requires a genuine, possibly-wrong choice). The resulting search discipline is formalized with a four-zone sequent `Δ; Ω ⇒ A; ·` / `Δ; Ω ⇒ ·; R`, where the *inner* zones (Ω, or the succedent-in-the-middle) are actively, eagerly decomposed and the *outer* zones (Δ, R) are "parked" synchronous propositions awaiting a deliberate choice. Soundness is immediate; completeness needs a battery of supporting lemmas — an **inversion lemma** (asynchronous rules may always be applied eagerly without losing completeness) and a **postponement lemma** (synchronous rules may always be delayed) — plus structural (weakening/contraction) properties for the newly ordered, non-idempotent zone Ω. **Termination of the asynchronous phase** is shown by a simple measure (the total logical connective/quantifier count of the active zone). The section ends with a genuinely non-deterministic — but now much more constrained — search procedure.

**Backchaining (§4.2)** specializes this discipline to **Horn logic**: theories built from clauses of the form `∀x₁...∀xₙ. P₁ ∧ ... ∧ Pₖ ⊃ P`. The key insight is that once you've decided *which* clause to try, you should apply *all* of its embedded quantifiers and implications in one committed sweep rather than re-opening the choice at every step — this collapses what would otherwise be a combinatorial explosion (the book computes it explicitly: naive inversion search on m clauses of arity n gives roughly `m(m+1)...(m+n)` choices, versus one m-way choice with backchaining). This is formalized as a **uniform-proof** judgment plus a **backchaining** judgment, proved sound and complete with a dedicated postponement lemma. A striking observation closes the section: backchaining on a Horn theory is *exactly* the same computation as reading the theory's clauses as ordinary inference rules and reasoning forward — connecting backward Horn-clause resolution to **forward chaining** / **unit resolution**, worked out concretely on a graph-reachability example. The book candidly flags the relationship between forward and backward strategies (and between the inverse method and resolution generally) as an **open research problem** at the time of writing.

**Focusing (§4.3)** generalizes backchaining's "commit and chase" discipline from Horn logic to the *entire* intuitionistic logic — this is presented as the single most important refinement in the chapter. The problem it solves: even after inversion collapses "don't-care" choices, a sequent with several available non-invertible assumptions still forces one quantifier/premise at a time to be resolved with a fresh disjunctive choice at *every* step, which is wildly more expensive than necessary (the book works out a concrete example where naively chasing two two-premise implications explodes into many redundant intermediate choice points). **Focusing** fixes this by requiring that once you decide to focus on a proposition (left or right), you chase a whole maximal chain of non-invertible connectives on *that one proposition* before considering anything else, only "blurring" the focus back to ordinary asynchronous decomposition once an invertible connective or an atom is reached. This needs four judgments (asynchronous right/left decomposition, and synchronous left/right focus) and a slightly finer classification in which conjunction and truth are allowed to be *either* synchronous or asynchronous depending on convenience — a wrinkle the book attributes to the fact that Andreoli's original focusing (developed for classical *linear* logic) didn't need this ambivalence, because linear logic has two distinct conjunctions (additive and multiplicative) each with a single fixed status. The section also connects focused proofs to Huang's "assertion-level" proofs (a format aimed at human-readable mathematical presentation) and to Herbelin's LJT calculus, noting that — unlike LJT — this focusing system is *not* in exact bijection with normal natural deductions, due to how the disjunction/⊥/∃ elimination rules interact.

**Unification (§4.4)** addresses **existential non-determinism**: the choice of witnessing term `t` when applying `∃`-right or `∀`-left. Rather than guessing `t` outright, the standard move is to substitute a fresh **existential (meta-/logic) variable** and defer the choice, checking only at the leaves (initial sequents) whether some substitution can make hypothesis and goal match — this deferred-check-and-solve technique is **unification**. The book formalizes this by **residuating** the choice into a companion "unification logic" formula `F` (built from atomic equalities, ∧, ⊤, ∃, ∀) attached to each sequent, proves a soundness/completeness pair connecting provability-with-residual-formula to ordinary provability, and then gives a concrete **unification algorithm** as a rewriting system on collections of equational constraints: structural decomposition of like function/predicate symbols, immediate failure on symbol clashes, and — critically — the **occurs-check**, which rejects unifying a variable `X` with a term that contains `X` (since no finite substitution could satisfy it). **Termination** and **preservation of satisfiability** are proved as the two halves of the algorithm's correctness. A historical note credits Herbrand with the first (footnoted) unification algorithm and Robinson with its introduction into automated deduction, followed by increasingly efficient (near-linear, then linear) algorithms.

**Unification with parameters (§4.5)** tackles a genuine subtlety: existential variables must not be allowed to depend on parameters that didn't exist when they were introduced (the canonical failing example being the invalid step from `∀x∃y. y=x` to the false `∃y∀x. y=x`). Two standard fixes are presented: **Skolemization** (replacing parameters with function terms over the currently-known existential variables, deferred to the exercises) and the book's preferred alternative — annotating every existential variable `X` with the exact set of parameters `∆` it's allowed to depend on (`X∆`), enforced by a **pruning** operation and a restriction judgment `t |∆` that rejects/restricts terms containing forbidden parameters before they're substituted in.

### 5. The Inverse Method

This chapter pursues the diametrically opposite search strategy to everything before it: instead of working backward from the goal, work **forward** from the axioms until the goal is derived. The chapter frames the trade-off precisely: forward search has *no* disjunctive non-determinism (knowledge only grows monotonically, nothing needs to be un-derived), but pays for this with potentially enormous **conjunctive non-determinism** — every applicable rule must eventually be tried on every derived sequent, so the central engineering problem becomes eliminating *redundancy*, not eliminating *choice*. The method is credited to Maslov, later adapted to non-classical logics by Voronkov, Mints, and Tammet.

**Forward sequent calculus (§5.1)** requires re-reading the sequent `Γ → C` as "*all* of Γ is needed to prove C" rather than "Γ is available." This single change of interpretation has real technical consequences: **weakening is no longer valid** (adding unneeded hypotheses would falsify the "all needed" reading), and hypothesis sets no longer need to track duplicates, so `Γ` becomes literally a set with union `∪` replacing the earlier "propagate Γ to both premises" pattern (e.g., `∧`-right unions the hypothesis-sets used to prove each conjunct, rather than sharing one Γ). Implication's right rule genuinely splits into two cases (whether `A` was actually used in proving `B`), foreshadowing later complications. Soundness is direct; **completeness is only recoverable up to a subset** (`Γ ⇒ C` implies `Γ' → C` for *some* `Γ' ⊆ Γ`) — the forward calculus's honest reflection of the fact that natural deduction allows unused hypotheses but the "needed" reading does not.

**Negation and empty succedents (§5.2)** reintroduces Gentzen's original device of allowing the right-hand side of a sequent to be *empty* (`Γ ⇒ ·`), interpreted as "Γ proves everything" — this cleanly sidesteps the propositional-parameter machinery §2.1 needed for negation, and is shown to be essential for a well-behaved forward calculus (the section systematically reworks every earlier rule, e.g. giving implication *three* right rules once the succedent may vanish).

**The subformula property (§5.3)** is what makes forward search feasible at all: in a cut-free proof of a goal sequent, *only subformulas of the goal* (and their substitution instances) can ever appear. This is sharpened into a **signed** subformula property by annotating every subformula with a polarity (positive/negative, tracking whether it inherits or flips sign through negations, antecedents of implications, etc.), yielding a search procedure: enumerate every signed subformula of the goal, generate corresponding initial sequents, then saturate by applying only those rule instances whose principal formula is a signed subformula of the goal, stopping on success (the goal sequent, or something that weakens to it, is derived) or on saturation without success.

**Naming subformulas (§5.4)** is a purely implementation-level optimization: rather than repeatedly re-scanning the goal for subformula occurrences, assign a name/label to every compound subformula once, and specialize the inference rules to operate directly on those labels.

**Forward subsumption (§5.5)** gives the propositional fragment a genuine decision procedure by formalizing when one derived sequent makes another redundant: `S` **subsumes** `S'` if `S'` follows from `S` by weakening alone, in which case `S'` need never be kept (or generated at all). The section also distinguishes this ("forward" subsumption, checked when adding a new sequent) from the rarer, more speculative "backward" subsumption (retroactively discarding previously-derived sequents made redundant by a new, more general one).

**Proof terms for the inverse method (§5.6)** notes a genuine wrinkle: because two-premise rules take the *union* of antecedent sets, naive proof-term labeling would need globally distinct variables to avoid interference between branches, and the book sketches (without fully resolving) both "on-line" (build proof terms as you go) and "off-line" (reconstruct only once a full derivation is found) strategies.

**First-order extension (§5.7)** generalizes everything to quantifiers, extending the subformula relation to an *immediate*-subformula relation `<` that accounts for arbitrary term/parameter instantiation, and works through detailed first-order examples — including one demonstrating that `∃y∀x.P(x,y) ⇒ ∀x∃y.P(x,y)` is derivable while its converse is *not*, the non-derivability falling directly out of a parameter side-condition violation at the one possible initial sequent.

**Factoring (§5.8)** exposes an outright **incompleteness** in the method as developed so far: a worked counterexample (`⊢ ∃x.P(x) ⊃ P(x) ∧ P(c)`) shows that sometimes a needed sequent is only a *contracted instance* of an already-derived (more general) one, and no rule so far performs that contraction after instantiation. The fix — **factoring**, an explicit "unify two antecedents of the same sequent and add the contracted result" rule — restores completeness.

**Inverse focusing (§5.9)** is the chapter's capstone: it combines the forward, subsumption/factoring-based search of §5.1–5.8 with the focusing discipline of §4.3, decomposing a goal down to a collection of independent **stable sequents** (sequents where everything remaining is synchronous) and then, for each stable sequent, *compiling* the focusing decomposition into a small, problem-specific set of derived inference rules and axioms — worked through several examples (propositional and first-order, including one deliberately unprovable case) that show forward reasoning saturating in very few steps once these derived rules are used. The section is explicitly flagged as more exploratory/speculative than the rest of the book (no full completeness proof is given), closing with a conjecture that factoring on stable sequents alone suffices.

### 6. Labeled Deduction

This chapter's organizing idea is to **relativize truth** to a *label* (informally, a "possible world"): instead of a single judgment "A true," we get a binary judgment "A true at p." The motivation given is to obtain a sequent calculus in which *every* rule is invertible — trading the disjunctive non-determinism seen in earlier chapters for bookkeeping over labels/worlds instead. Wallen's book is cited as the foundational reference for this technique in automated deduction.

**Multiple conclusions (§6.1)** is a warm-up: replace a single-succedent sequent with a genuinely classical-looking multiple-conclusion judgment `Γ ⇒ᵐ Δ` ("prove one of Δ"), reusing rules essentially identical to the classical `Γ # Δ` judgment of §3.7 for ∧/∨, but this immediately breaks intuitionistic soundness for implication — the book gives an explicit derivation of the (classically valid, intuitionistically invalid) `(A ⊃ B) ∨ A` that exploits an illegitimate sharing of information between disjuncts through the naive `⊃`-right rule. The fix is a corrected `⊃`-right rule that *commits*, discarding the rest of Δ, exactly when the new hypothesis is introduced — restoring intuitionistic soundness at the cost of making that one rule non-invertible again in a controlled way. Soundness now only guarantees that *some disjunction* of Δ is provable (not that any single member is), a subtlety the book proves carefully.

**Propositional labeled deduction (§6.2)** replaces the "commit" behavior above with explicit **labels** — finite sequences of label parameters — such that a hypothesis introduced at label `p` remains available to prove any conclusion at any *extension* `pq` of that label (this is literally how "scope" is formalized: as an ordering on labels). The `⊃`-right rule creates a *fresh* label parameter for the new hypothesis, which automatically prevents it from leaking into unrelated branches of the succedent, without needing to erase anything. Soundness/completeness (via a notion of a **monotone** sequent, where every left-label is a prefix of every right-label) are established, with the book noting candidly that the completeness direction is comparatively easy while soundness is "considerably more difficult," typically requiring either Kripke-model arguments or direct translation to/from matrix proofs — pointing to Wallen, Waaler, and Schmitt et al. for the full treatment.

**First-order labeled deduction (§6.3)** extends the same idea to quantifiers, since universal quantification *also* introduces a new scope in intuitionistic logic (not just implication) — this requires labeling *terms* as well as propositions (a term is only "well-formed at" the labels where its constituent parameters were introduced), tracked via a labeled parameter context.

**Matrix methods (§6.4)** is a brief pointer chapter: once labels and terms are both handled via free variables and unification (as in Chapter 4, but now unifying *labels* too), the resulting search techniques are the **matrix/connection/mating methods** originally developed for classical logic — the book explicitly defers the details to Waaler's survey and Wallen's book rather than developing them in full.

### 7. Equality

The final chapter shows how to reason about equality *efficiently* rather than merely *soundly*: simply adding reflexivity/symmetry/transitivity/congruence as axioms works, but produces a hopelessly large search space, so the chapter re-derives equality's proof theory from first principles, exactly as earlier chapters did for the logical connectives.

**Natural deduction for equality (§7.1)** gives a single introduction rule (**reflexivity**, `s = s`) and — perhaps counterintuitively — *two* elimination rules, one that lets you replace occurrences of `s` by `t` in a true proposition given `s = t`, and one that replaces `t` by `s`. The book proves the second elimination rule is technically *derivable* from the first (via a short detour through reflexivity), but is still indispensable to keep: without it as a *primitive*, the normalization theorem fails and cut elimination for equality breaks down, because the derivable version isn't a *normal* deduction. This is a small but important lesson repeated from the philosophy of the whole book: local completeness (having *some* way to reconstruct a connective from its eliminations) does not automatically give you *global* completeness of a restricted, normal-form-only system — you sometimes need to add rules that are provably redundant at the level of raw derivability but not at the level of *normal* derivability. Proof terms follow the same bidirectional (checked/synthesized) discipline as Chapter 3's compact proof terms, introducing `refl` and two `subst` constructs annotated with enough information (the motive proposition and bound variable) to keep type synthesis unique.

**Sequent calculus for equality (§7.2)** hits a genuine technical obstacle: the natural left-rules for equality change the *principal formula* under a substitution when cut is pushed past them, which breaks the usual cut-admissibility induction outright (the book shows the exact failure case). The repair is to **restrict** the equality rules so they can only be applied last, to atomic formulas — pushing all equational reasoning to the leaves of a derivation and cleanly separating it from ordinary logical reasoning. This is formalized with two new judgments, an **equational derivation** (`⇒ᴱ`) that only ever manipulates atoms/equalities, and a **regular derivation** (`⇒ᴿ`) that uses all the usual logical rules plus one coercion from equational derivations — after which soundness is immediate, and completeness needs a substitution-generalization lemma (equality rules remain admissible even under simultaneous substitution into the surrounding context) plus a small lemma establishing atomic initial sequents by structural induction. The chapter, and the book, close with a four-part **Admissibility of Cut with Equality** theorem, restoring — for the extended logic — exactly the central result (§3.4) the whole book was built to generalize.

---

## Why the book is organized this way

Stepping back, the throughline across all seven chapters is a single recurring *pattern of argument*, applied at increasing levels of refinement:

1. Define a proof-search discipline as a *restricted* judgment (normal deductions, sequents, focused sequents, forward sequents, labeled sequents, equational/regular derivations).
2. Prove it **sound** with respect to the previous, more permissive system (usually easy, by direct induction).
3. Prove it **complete** (usually hard, often requiring an extra bridging system, a generalized induction hypothesis, or an admissibility/cut-elimination argument).
4. Show the extra machinery used to bridge soundness and completeness (the `↓⇑` coercion, the cut rule, unification's residual formulas, factoring) is in some precise sense *redundant* — which is exactly what licenses treating the restricted system as a genuine decision procedure or search algorithm rather than just another equivalent formulation.

Each chapter's "new" proof-search idea (sequent calculus, then focusing, then the inverse method, then labeling, then equality) is not an ad hoc trick but a specific answer to a specific inefficiency exposed by the previous chapter — which is why the book reads less like a survey of unrelated techniques and more like a single sustained derivation.
