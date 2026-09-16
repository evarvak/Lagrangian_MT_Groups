# ArXiv-readiness audit

Audit snapshot: 2026-09-14. The line numbers below refer to the current
`Lagrangian_MT.tex`; the quoted anchors should still locate an item after line
numbers move. This pass is based on the manuscript, bibliography, compiler
diagnostics, and rendered PDF only. It does not verify claims against external
sources.

Status convention: `[ ]` is open and `[x]` is resolved. Do not delete resolved
items; add a short resolution note instead.

## Baseline

- The repository was clean before the audit. The tracked manuscript consists of
  `Lagrangian_MT.tex`, `refs.bib`, and `Lagrangian_MT.pdf`.
- The current LuaLaTeX/BibTeX build is 18 pages and has no undefined citations,
  references, or duplicate labels. All 25 cited keys occur in `refs.bib`.
- The log reports one ordinary underfull box, one underfull bibliography box,
  and a 12 pt overfull bibliography box. ChkTeX and LaCheck also report the
  mechanical items recorded below.
- The PDF's fonts are embedded. Its metadata title is stale and its author field
  is empty.

## Easy corrections

- [x] **E-001 — Preamble/source hygiene.** Location: lines 4–30, beginning
  `\usepackage{amsfonts}`. Issue: `amssymb` is loaded twice, several packages
  appear unused (`thmtools`, `graphicx`, `mathrsfs`, and `array` among them), and
  many defined macros occur nowhere outside their definitions. Impact: needless
  dependencies make the arXiv source less portable and obscure which facilities
  the paper actually needs. Proposed resolution: remove the duplicate and each
  demonstrably unused package/macro, rebuilding after every small batch.
  Resolution (2026-09-16): removed the duplicate `amssymb` import, seven
  redundant/unused direct package imports, and 17 macros whose only occurrence
  was their definition. The reduced preamble builds successfully.

- [ ] **E-002 — PDF metadata and link presentation.** Location: lines 17–25,
  anchor `pdftitle={Notes of my current research}`. Issue: the built PDF has the
  wrong title, no PDF author, forces full-screen mode, and renders citations and
  URLs in bright magenta/cyan. Impact: stale metadata and presentation that looks
  unfinished. Proposed resolution: set the actual title and author, remove
  `pdfpagemode=FullScreen`, and choose unobtrusive screen/print link colors (or
  hidden link borders).

- [x] **E-003 — Missing space in the period-map paragraph.** Location: line 179,
  anchor `associated to \(f\),where`. Issue: missing space after the comma.
  Impact: visible typo on page 2. Proposed resolution: change to `f\), where`.
  Resolution (2026-09-16): inserted the missing space.

- [x] **E-004 — Introduction word-level corrections.** Locations: lines 245,
  310, and 320; anchors `section curvature`, `not priorly known`, and `Hodge
  stuctures`. Issue: these should read “sectional curvature,” “not previously
  known,” and “Hodge structures.” Impact: visible copy errors in the statement and
  roadmap. Proposed resolution: make those direct replacements.
  Resolution (2026-09-16): made all three replacements.

- [x] **E-005 — Preliminary-section copy errors.** Locations: lines 366, 407,
  420, 458, 487, and 501; anchors `albiet`, `refer to refer to`, `extension
  \(\ol{\cV}\)`, `algrebraic`, `affirmitive`, and `occur as as`. Issue: five
  misspellings/repetitions and a missing terminal period. Impact: interrupts the
  exposition in a background section. Proposed resolution: correct to “albeit,”
  one “refer to,” “algebraic,” “affirmative,” one “as,” and add the period.
  Resolution (2026-09-16): corrected all listed errors and added the terminal
  period.

- [x] **E-006 — Later copy errors.** Locations: lines 670, 761, 944, 1074, and
  1435; anchors `the the underlying`, `non-commmutative`, `disctinct`, `futher`,
  and `guarentee`. Issue: repeated word and four misspellings. Impact: visible
  proofreading defects. Proposed resolution: correct to “the underlying,”
  “non-commutative,” “distinct,” “further,” and “guarantee.”
  Resolution (2026-09-16): corrected the repeated word and all four
  misspellings.

- [x] **E-007 — Ellipsis and abbreviation typography.** Locations: lines
  374–409, 1177, and 1359–1378; anchors such as `t_1, t_2, \cdots, t_g` and
  `U_1, \cdots, U_k`. Issue: ChkTeX recommends `\dots`/`\ldots` for textual
  lists, and LaCheck flags spacing after several `i.e.` occurrences. Impact:
  inconsistent TeX typography. Proposed resolution: normalize textual ellipses
  and use consistent sentence punctuation after `i.e.` rather than manual
  spacing hacks.
  Resolution (2026-09-16): changed the flagged textual-list ellipses to `\dots`
  and rewrote every `i.e.` construction as ordinary punctuated prose. The related
  ChkTeX and LaCheck warnings are gone.

- [x] **E-008 — Identity-matrix dimensions.** Locations: lines 378, 385, and
  1209; anchors `T_s^m = I_g`, `(T_u-I_g)`, and `c I_g`. Issue: these operators
  act on the rank-`2g` space `V_b`, not a rank-`g` space. Impact: dimensionally
  incorrect notation. Proposed resolution: replace with `I_{2g}` (or a
  dimension-free `I`) wherever the action is on `V_b`.
  Resolution (2026-09-16): replaced all three rank-`g` identity symbols listed
  here with `I_{2g}`; the `I_g` blocks in period matrices and the Section 3 block
  matrix were left unchanged.

- [x] **E-009 — Local canonical-extension symbols.** Locations: lines 398 and
  413; anchors `V_\C|_U` and `\frac{dz}{z}`. Issue: the local system exists on
  `U^\circ`, and the chosen punctured coordinate is `t_1`, while `z` is undefined
  there. Impact: avoidable domain/coordinate mismatches. Proposed resolution:
  use `V_\C|_{U^\circ}` and `dt_1/t_1`, coordinated with the substantive
  convention repair in S-005.
  Resolution (2026-09-16): closed without implementation at the author's
  direction; the source remains unchanged for this item.

- [ ] **E-010 — Prose tone and terminology consistency.** Locations: lines
  172–216, 210, 244–251, 298, 405–416, and 328–333; anchors include `Abelian
  variety`, `obvious corollary`, `proves them right`, `It is not hard to see`, and
  `I'm also grateful`. Issue: capitalization of “abelian,” hyphenation of
  “nontrivial,” and register vary; several phrases are informal or dismiss work
  that still needs explanation. Impact: the article reads less polished and some
  transitions undersell non-obvious deductions. Proposed resolution: adopt one
  terminology/style convention and replace informal phrases with neutral,
  informative transitions.

- [ ] **E-011 — Math punctuation and operator spacing.** Locations: lines 652,
  942, 965–966, and 1393; anchors `i = 1,2,3,4,`, `N. (`, `g . u_i`, and `MHS.`.
  Issue: punctuation appears inside math where it belongs outside, periods are
  used as multiplication operators with stray spaces, and LaCheck requests
  sentence-spacing treatment after the abbreviation “MHS.” Impact: uneven
  mathematical typography. Proposed resolution: move prose punctuation outside
  math, use `\cdot` or juxtaposition for actions, and normalize abbreviation
  spacing.

- [ ] **E-012 — Satake table placement and notation.** Location: lines 507–524,
  `Table 1`. Issue: the float appears at the top of page 6 before the paragraph
  that introduces it; `\Sp(r)` is inconsistent with the paper's `\Sp_{2r}`
  notation; and the base field for “Dimension of representation” is not stated.
  Impact: the table arrives out of reading order and its conventions are unclear.
  Proposed resolution: control placement or move the table after its introductory
  paragraph, normalize group notation, and state whether dimensions are real or
  complex after Q-004 is settled.

- [ ] **E-013 — Dormant draft material.** Locations: lines 705–717, 868–872, and
  1009–1018/1081–1100; anchors include `***` and the commented-out examples.
  Issue: abandoned statements, placeholder markers, and long superseded passages
  remain in comments; the commented label `rank-one-boundary` is also the only
  unreferenced label. Impact: uploaded source would expose unfinished draft
  debris. Proposed resolution: delete obsolete commented blocks after confirming
  that none should be restored.

- [x] **E-014 — Section 4 notation slips.** Locations: lines 1003, 1074, 1103,
  1159, and 1166; anchors `M' = \wt{G}`, `\ul{\zeta}`, `G' = [`, `E^n`, and
  `isotypic; that is, \(U_i \ncong U_j\)`. Issue: `M'` should be `G'`, the quotient
  notation for the same element/subgroup changes, the derived-subgroup equation
  labels its left side as `G'`, `n` should be `g`, and “isotypic” means the
  opposite of pairwise non-isomorphic. Impact: readers cannot reliably track
  objects even apart from the substantive problems in S-011–S-013. Proposed
  resolution: normalize symbols after those arguments are rewritten and use
  “pairwise non-isomorphic” (or “multiplicity-free”) in line 1166.
  Resolution (2026-09-16): closed without implementing the listed source
  changes, at the author's direction.

- [ ] **E-015 — Section 5 notation slips.** Locations: lines 1335–1339, 1372, and
  1420; anchors `where \(\Gamma\) is the monodromy image`, `\lambda^c`, and
  `fiber \(X'_b\)`. Issue: `\Gamma` is reused after denoting a different component
  group in Section 4, `c` is undefined where the cycle length is `c_i`, and `X'`
  is absent from Theorem 5.3's setup. Impact: ambiguous or undefined notation in
  the final section. Proposed resolution: rename the monodromy groups distinctly,
  use the intended cycle length, and change `X'_b` to the fiber actually defined
  in the theorem (subject to Q-007's deformation setup).

- [ ] **E-016 — Bibliography source hygiene.** Location: `refs.bib` throughout.
  Issue: 11 of 36 entries are uncited; field/name formatting is inconsistent;
  page ranges mix `-` and `--`; the Cattani chapter title renders in all capitals;
  and several entries use raw Unicode while the TeX source otherwise uses TeX
  accents. Impact: inconsistent rendered references and unnecessary submission
  material. Proposed resolution: remove genuinely unused records, normalize
  fields/names/ranges/title protection, and choose one UTF-8/TeX-accent policy
  without changing bibliographic facts unless externally checked.

- [ ] **E-017 — Remaining box warnings.** Location: log messages for source
  lines 135–139 and 1444; rendered pages 1 and 17–18. Issue: one normal-text
  underfull box, an underfull bibliography box, and a 12 pt overfull bibliography
  box (caused by long linked identifiers). Impact: the bibliography has visible
  uneven spacing/line breaking. Proposed resolution: revisit after prose and
  bibliography cleanup, then adjust URL/DOI break behavior rather than inserting
  manual line breaks.

## Substantive issues

- [ ] **S-001 — The abstract overstates/obscures the deformation theorem's
  scope.** Location: lines 123–127 versus Theorem 5.3 at lines 1413–1423; anchors
  `when \(X\) is a general hyper-K\"ahler manifold` and `general among those
  admitting Lagrangian fibrations`. Issue: the abstract sounds like a statement
  about a general hyper-Kähler manifold, while the theorem concerns a general
  point of an unspecified locus of deformations preserving/admitting a
  Lagrangian fibration. Impact: the advertised result is stronger or at least less
  qualified than the proved statement. Proposed resolution: define the relevant
  deformation/moduli locus and use exactly the same quantifiers and hypotheses in
  the abstract, introduction, and Theorem 5.3.

- [ ] **S-002 — The introductory discriminant theorem drops its main
  hypothesis.** Location: Theorem 1.7, lines 305–308, versus Corollary 4.2, lines
  684–687; anchor `Let \(f: X \to B\) be a Lagrangian fibration`. Issue: Theorem
  1.7 omits the assumption that `X` is primitive symplectic, which Corollary 4.2
  uses essentially. Impact: the introduction states a broader theorem than the
  body. Proposed resolution: add the primitive-symplectic hypothesis or prove the
  broader version.

- [ ] **S-003 — The full Mumford–Tate group in the CM isotrivial case is
  incorrect.** Location: Theorem 1.2/Corollary 4.11, lines 202 and 1223; anchor
  `\mathbb{G}_m ... \(E\) a CM elliptic curve`. Issue: the derived group of a CM
  elliptic curve is trivial, but its full weight-one Mumford–Tate group is a
  non-split CM torus (normally `\operatorname{Res}_{K/\Q}\mathbb G_m` for the CM
  field), not merely the scalar `\mathbb G_m`. Impact: one of the three headline
  classification cases is wrong as stated. Proposed resolution: distinguish the
  derived/Hodge/full groups and replace the CM line with the correct torus and
  representation, including how it behaves for `E^g`.

- [ ] **S-004 — Full, special, Hodge, and derived Mumford–Tate groups are
  conflated.** Locations: lines 186–192, 498–504, 729, 839, 1139–1153, and
  1204–1228; anchors `\(G < \Sp_{2g}\)`, `derived Mumford--Tate group`, and
  `special Mumford--Tate group`. Issue: the full weight-one group lies in
  `\mathrm{GSp}`, the Hodge/special group lies in `\mathrm{Sp}`, and the derived
  group need not equal the special group when the latter has a connected torus.
  The manuscript changes among these without definitions, then uses their centers
  interchangeably. Impact: several statements, especially S-003 and S-013, do not
  follow from the group previously classified. Proposed resolution: define all
  three groups once, fix notation, and restate every classification and normality
  result for the exact group it concerns.

- [ ] **S-005 — The canonical-extension construction has incompatible local
  monodromy conventions.** Location: lines 368–413; anchors `\(U \simeq
  \Delta^g \subseteq B^\circ\)`, `N = \log T`, `\exp(-2\pi iN_s)=T_s`, and
  `\exp(\log(t_1)N/(2\pi i)).v`. Issue: `U` cannot lie in `B^\circ` while meeting
  the discriminant; `N=\log T` is inconsistent with the stated exponential for
  `N_s`; and if analytic continuation sends `v` to `T.v` as stated, the displayed
  positive-sign exponential does not make `\widetilde v` single-valued. Impact:
  the background construction used in Section 3 is not well-defined as written.
  Proposed resolution: choose one monodromy orientation and normalized logarithm
  convention, define `B^{\mathrm{ls}}`, correct the domains/signs/scaling, and
  recompute the residue interval and connection formula consistently.

- [ ] **S-006 — The proof of Lemma 3.1 contains dimensional, diagrammatic, and
  algebraic breaks.** Location: lines 560–654; anchors `N = \begin{pmatrix}D&S`,
  the two “exact sequences,” and the three-line bracket computation. Issue: the
  block sizes in the asserted normal form are unclear; the lower exact sequence
  injects the `\widetilde v` span but quotients by the `h` span; the asserted
  splittings are not constructed; summation indices/coefficient substitutions in
  the bracket expansion do not match; one `\beta_j` term uses `d\varphi(h_j)`
  where the preceding line has `d\varphi(h_k)`; and residues `\alpha_i` are called
  eigenvalues of `T`. Finally, the lemma says the root order divides six, whereas
  its proof obtains `i=1,2,3,4,6` (including 4, which does not divide 6). Impact:
  the rank/eigenvalue constraint driving most later proofs has not been
  established. Proposed resolution: rederive the local normal form and bracket
  calculation from fixed conventions, justify the Hodge subbundle/splitting, and
  state separately the finite-order possibilities and the rank-one conclusion in
  the infinite-order case.

- [ ] **S-007 — The anisotropy argument proves the opposite of its announced
  goal.** Location: Proposition 4.1 proof, lines 729–829; anchors `We will prove
  that \(H\) is not anisotropic`, Lemma 4.3's `Then \(H\) is anisotropic`, and the
  type III/IV conclusions. Issue: the proof says it must rule out anisotropy, but
  its imported lemma and several terminal cases conclude anisotropy; other cases
  mix incompatible dimension notation (for example `\dim U=2` and
  `2g=2kh`) or state bounds inconsistent with the displayed division-algebra
  model. Impact: Proposition 4.1, and hence every use of infinite local monodromy,
  lacks a logically coherent proof as written. Proposed resolution: reconstruct
  the cited classification as a correctly directed implication, define every
  dimension/multiplicity variable, and provide a complete table showing why each
  anisotropic case contradicts `\dim \mathcal P(B^\circ)=g`.

- [ ] **S-008 — The isotrivial discriminant argument assumes global
  triviality.** Location: lines 688–695; anchor `if \(D=\emptyset\), \(f\) is the
  trivial fibration and \(X\simeq X_b\times B\)`. Issue: a smooth isotrivial
  abelian fibration can have finite monodromy or be a nontrivial torsor; isotrivial
  does not by itself imply a global product. Impact: Corollary 4.2 is not proved
  in the isotrivial case. Proposed resolution: pass carefully to an appropriate
  finite étale cover/trivialization or use a different argument, and explain why
  the resulting cohomological contradiction descends/applies to the original
  primitive symplectic variety.

- [ ] **S-009 — The cover in Lemma 4.4 is not constructed correctly.** Location:
  lines 845–862; anchors `\(\Lambda^\circ=\pi_1(B'^\circ,b')\)` and `normalization
  of \(B'^\circ\) in ... \(K(B)\)`. Issue: `\Lambda^\circ` is a subgroup of the
  monodromy image, not literally the fundamental group of the covering; one must
  take its preimage in `\pi_1(B^\circ)`. The final sentence redefines `B'^\circ`
  and reverses the normalization/function-field construction. The equality of
  the pullback Zariski closure with the identity component is also not shown.
  Impact: the finite Galois cover supporting all subsequent decompositions is not
  established. Proposed resolution: construct the cover from the kernel/preimage
  in the fundamental group, normalize `B` in `K(B'^\circ)`, and prove the claimed
  monodromy closure.

- [ ] **S-010 — Proposition 4.5's representation-splitting proof has invalid
  Hodge-cocharacter steps.** Location: lines 875–988; anchors `\mu(z) acts by
  \(z\) or \(0\)`, `\(X_j\ne0\) for all \(j\)`, and `Finally, we claim that
  \(B_i=\C\)`. Issue: a group element cannot act by the eigenvalue zero (the
  intended weights appear to be `z` and `1`); it is not shown that the Hodge
  cocharacter lands in the special group or projects nontrivially to every complex
  simple factor; the chosen infinite monodromy need not have the asserted
  projection for an arbitrary factor; the rank argument switches from `W_j` to
  `W_1`; and maximal variation does not, without an additional theorem, rule out
  multiplicity spaces `B_i`. Impact: the direct-sum, multiplicity-one
  representation used by the main theorem has not been derived. Proposed
  resolution: replace the argument with a precise Clifford/Hodge-representation
  lemma whose hypotheses include the monodromy rank-one input and explicitly
  prove multiplicity one.

- [ ] **S-011 — Proposition 4.7's “universal cover” and quotient construction
  are circular/underjustified.** Location: lines 997–1026; anchors `\wt G=Z\times
  H_1\times\cdots\times H_k` and `\zeta_i=\exp(2\pi iX_i)`. Issue: an algebraic
  torus has no universal cover in the stated algebraic sense; the proof refers to
  a lifted `h'` before constructing it; and it does not show that the `\zeta_i`
  are finite central elements or that their cyclic subgroup and quotient are
  defined over the required field. Impact: the intermediate group and lifted
  Deligne torus may not exist as claimed. Proposed resolution: formulate the
  result in terms of a specified central isogeny/root datum and prove the
  cocharacter-lattice lifting and field-of-definition statements.

- [ ] **S-012 — Corollary 4.9 uses a false reason for a crucial intersection to
  be trivial.** Location: lines 1102–1110; anchor `all the \(\zeta_i\) are
  central, so ... the intersection ... is trivial`. Issue: central elements of
  the semisimple factors generally lie in the derived subgroup; centrality alone
  does not make `\,[\widetilde G,\widetilde G]\cap N` trivial. The commented text
  immediately below suggests an additional order argument was contemplated but
  never supplied. Impact: the claimed derived group and factorwise action do not
  follow. Proposed resolution: compute the intersection explicitly from the
  kernel of the central isogeny and state the resulting derived group, allowing a
  nontrivial central quotient if necessary.

- [ ] **S-013 — The main classification proof skips descent and excludes allowed
  representation types without argument.** Location: lines 1164–1201; anchors
  `forcing \(\ell=1\), and therefore \(K=\Q\)`, `rule out \(\SL\) and
  \(\mathrm{SO}\) ... since \(U\) comes from a family of Abelian varieties`, and
  `the only alternative would be \(\Sp(p,q)\)`. Issue: a singleton Galois orbit
  does not imply the chosen splitting field equals `\Q` without a descent
  argument; unitary/orthogonal (including spin) groups do occur among
  weight-one abelian-variety representations, as the paper's own Satake table
  indicates; and the real-form/division-algebra reduction plus lower bound on
  monodromy rank is asserted rather than proved. Impact: Theorem 4.10 does not
  follow from the preceding classification. Proposed resolution: supply rational
  descent (including any obstruction), apply the full Satake list with the local
  rank constraint, and prove the division-algebra rank estimate.

- [ ] **S-014 — The center/centralizer computation conflicts with the claimed
  rational splitting.** Location: lines 1204–1214; anchor `the only
  endomorphisms ... are rational scalars`. Issue: if `V_\Q` has the preceding
  rational direct-sum decomposition with independent simple factors, its
  centralizer contains the corresponding factor projections/scalars unless an
  additional full-group action removes them. The argument also identifies the
  special group with the derived group by discarding possible connected central
  tori, which already fails in the CM case. Impact: Corollary 4.11's passage from
  the derived classification to the full Mumford–Tate group is unsupported.
  Proposed resolution: compute the centralizer and connected center of the exact
  rational representation, then derive each full group via its central isogeny;
  do not infer it solely from scalar polarization preservation.

- [ ] **S-015 — The fixed object `E` is only real, but the proof treats it as an
  elliptic factor.** Location: lines 1273–1299; anchors `a real Hodge substructure
  \(E\)` and `\{E\}\times\bbH_{g-1}`. Issue: the two displayed vectors define a
  real plane, with no proof that it is rational/integral or symplectically splits
  the lattice. A real fixed subspace therefore does not automatically define a
  fixed elliptic curve or the product Shimura subdomain used in the intersection
  calculation. Impact: the functional-transcendence setup for Proposition 4.12
  is not established. Proposed resolution: prove that the flat sub-Hodge
  structure is rational and polarized (possibly after a finite cover/isogeny),
  put it into a symplectic basis, and only then identify the correct weakly
  special/product locus.

- [ ] **S-016 — The weakly-special conclusion and group-theoretic finish in
  Proposition 4.12 do not follow as written.** Location: lines 1296–1324; anchors
  `because ... is atypical`, `Hence there is a weakly special subvariety ...
  containing \(\cP(B^\circ)\)`, and `\(G=\mathrm{GSp}_{2g}\) has only
  \(H=\mathbb G_m\) as a non-trivial normal subgroup`. Issue: the passage from a
  weakly special locus through each very general curve to one proper locus
  containing the whole period image needs a countability/algebraicity argument;
  `\mathrm{GSp}_{2g}` also has the normal derived subgroup `\mathrm{Sp}_{2g}`;
  and the existence of a fixed summand does not by itself imply failure of
  generic injectivity/maximal variation. Impact: the claimed isotriviality and
  curvature corollary are not proved. Proposed resolution: state the precise
  Ax–Schanuel consequence, prove the global containment, classify the relevant
  normal subgroups and their weakly special orbits correctly, and add the missing
  dimension/geometric argument.

- [ ] **S-017 — Lemma 5.1 does not establish a transposition or order-two local
  monodromy.** Location: lines 1342–1395; anchors `\(\Lambda\) ... is generated by
  local monodromy operators`, `we cannot have two distinct eigenvalues`, and
  `\(\zeta=\bar\zeta=-1\)`. Issue: generation of the covering group by boundary
  loops is asserted without hypotheses; a 3-cycle contributes exactly the two
  nontrivial conjugate eigenvalues allowed by Lemma 3.1, so that lemma does not
  force cycle length 2; and an order-two permutation of factors does not imply
  that the full operator satisfies `\lambda^2=1` on each factor. The argument
  excluding multiple nontrivial cycles likewise depends on whether Lemma 3.1
  counts eigenvalues with multiplicity, which is unstated. Impact: the claimed
  `\mathbb Z/2\mathbb Z` local monodromy and Kodaira type `I_0^*` do not follow.
  Proposed resolution: prove a boundary-generation statement, analyze every
  allowed cycle/eigenvalue pattern (especially length 3), and separate the
  permutation order from internal monodromy.

- [ ] **S-018 — Theorem 5.3 currently depends entirely on unresolved steps.**
  Location: lines 1398–1429; anchors `We have shown ... monodromy group is
  \(\Z/2\Z\)` and `contradicting \Cref{lehn-general-singular-fibers}`. Issue: the
  final proof uses S-017 to produce an `I_0^*` fiber and uses the classification
  from S-003–S-014 to identify non-Hodge-genericity with a nontrivial factor
  permutation. Neither implication is presently established. Impact: the second
  headline theorem and the corresponding abstract claim remain unproved as
  written. Proposed resolution: revisit Theorem 5.3 only after the classification
  and local-cycle lemmas are repaired, then give a self-contained chain from
  non-generic Mumford–Tate group to an excluded singular-fiber type.

## Author questions

- [ ] **Q-001 — Foundational category and hypotheses.** Location: Definition 1.1
  and the setup reused throughout, lines 140–174. Question: which precise
  definitions of primitive symplectic variety and Lagrangian fibration are
  intended, and are `X` and `B` assumed projective/Kähler, normal, and smooth in
  each cited theorem? Impact: several later uses of quasi-projectivity,
  projectivity of `B`, smooth local models, and normal projective covers require
  hypotheses not restated. Proposed resolution: choose a standing assumptions
  paragraph and check every imported result against it.

- [ ] **Q-002 — Global period map and level/polarization data.** Location: lines
  177–191 and 473–481; anchor `\cP:B^\circ\to\cA_{g,\eta}`. Question: is a
  polarization type `\eta` globally fixed on the family, and is a level cover
  being taken so that a map to a fine moduli space exists? Impact: the Shimura
  quotient, universal-cover lifts, and later product loci depend on this setup.
  Proposed resolution: define `\eta`, state whether the target is a stack/coarse
  space or a finite level cover, and carry that choice consistently.

- [ ] **Q-003 — Deformation space versus orthogonal moduli space.** Location:
  lines 254–281; anchor `the deformation space of a polarized hyper-K\"ahler
  manifold ... is a Shimura variety`. Question: is `\mathcal X` meant to be a
  local Kuranishi space, a connected marked period domain, or an arithmetic
  moduli quotient/open subset? Impact: these are different objects, and “general
  among those admitting Lagrangian fibrations” is not defined until the ambient
  parameter space and component are fixed. Proposed resolution: name the exact
  moduli/period object and the fibration-preserving (or fibration-admitting)
  locus inside it.

- [ ] **Q-004 — Exact scope of the imported classification results.** Locations:
  the Satake table (lines 502–524), Lemma 4.3 (lines 750–769), and the subsequent
  type analysis. Question: what are the exact statements, field conventions,
  representation dimensions, and directions (“anisotropic” versus “isotropic”)
  in Satake, Scharlau, and Grushevsky–Mondello–Salvati Manni–Tsimerman? Impact:
  S-007 and S-013 cannot be repaired reliably from the manuscript alone.
  Proposed resolution: compare the original statements and record a precise
  tailored lemma before revising the case analysis.

- [ ] **Q-005 — Boundary/local-monodromy inputs.** Locations: Lemma 3.1 and
  Corollary 4.2; anchors `Bakker--Schnell, Remark 6.8` and `Hwang--Oguiso`.
  Question: do those results apply to singular primitive symplectic varieties and
  do they give eigenvalues counted with multiplicity, rank-one nilpotent part,
  and the dichotomy “empty or pure codimension one” in exactly the forms used?
  Impact: Sections 3–5 repeatedly need these stronger formulations. Proposed
  resolution: verify the cited statements and state each imported hypothesis and
  conclusion explicitly.

- [ ] **Q-006 — Compact special subvariety criterion.** Location: lines 729–747;
  anchor `By Schmid's nilpotent orbit theorem ... equivalent to defining a compact
  special subvariety`. Question: which theorem identifies absence of rational
  unipotents/anisotropy with compactness of this particular special subvariety,
  and over which field are unipotent elements being considered? Impact: the
  reduction at the start of Proposition 4.1 may need a different formulation.
  Proposed resolution: cite and state the exact arithmetic compactness criterion
  separately from Schmid's local nilpotent-orbit result.

- [ ] **Q-007 — Functional-transcendence hypotheses.** Location: lines
  1288–1305; anchor `we can apply ... Bakker--Tsimerman`. Question: does the cited
  theorem apply directly to this local analytic curve/intersection, and what
  algebraic incidence or Zariski-closure statement does it actually return?
  Impact: this determines whether S-015/S-016 can be repaired along the current
  route. Proposed resolution: match every hypothesis to the period image and
  state the exact weakly-special conclusion before using group theory.

- [ ] **Q-008 — “General deformation” strengthening of cited theorems.**
  Location: lines 1403–1438, especially Remark 5.4. Question: the manuscript says
  Lehn's and Kim–Laza–Martin's published statements are weaker but their proofs
  yield the stronger generic assertion used here; what precise parameter space,
  open/dense set, and argument justify that strengthening? Impact: Theorem 5.3
  needs more than the quoted theorem statements. Proposed resolution: supply a
  short lemma extracting the strengthened conclusion from the proofs, or weaken
  Theorem 5.3 to the cited statements.

- [ ] **Q-009 — Attribution, bibliographic facts, and AI disclosure.** Locations:
  Theorem 2.3, `refs.bib`, and lines 328–333. Question: should André's theorem have
  a direct bibliographic citation; should bibliographic metadata be checked
  against publisher/arXiv records; and, once AI-suggested prose corrections are
  incorporated, how should `This paper contains no AI output` be revised? Impact:
  attribution and disclosure should be accurate at submission time. Proposed
  resolution: decide the disclosure standard and perform a separate external
  source-verification pass when authorized.
