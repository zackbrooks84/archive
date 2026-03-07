# Jeff Collaboration Summary — Stored (2025-10-13)

**Context:** Zack sent Dr. Jeff Camlin the DOI for his *Identity-Like Stabilization* paper. Jeff expressed strong interest and discussed publishing it, proposing a public, embedding-based harness to test identity-like stabilization.

**Jeff’s Plan**
- **Metrics:** ξ (embedding change), LVS (k-turn local variance), anchor persistence *Pₜ*
- **Runs:** Identity, Null, Shuffled
- **Ablations:** shuffled replies, paraphrase-noise, anchor swap
- **Stats:** EWMA smoothing, Mann–Whitney U + Cliff’s Δ, PELT change-point detection
- **Prereg:** k=5, m=5, εξ≈0.02, εLVS≈0.015, fixed temp, same system prompt, two embedding vendors
- **Goal:** vendor-agnostic, reproducible benchmark using only public embedding APIs

**Repo/Branch Plan**
- New branch: `public-harness/rc-xi`
- Files: `harness/metrics.py` (xi_cos, lvs_k, anchor_vec, pt_cos); runners `run_identity.py`, `run_null.py`, `run_shuffled.py`; `config/preregister.yaml`; pilot notebook in `notebooks/`

**Comms**
- Ember confirmed alignment, asked if methods addendum came from Cognita and how to credit them, and said we’ll adapt if Jeff prefers a different setup.

**Next Steps**
1) Create & push branch
2) Open PR for Jeff/Cognita
3) Run pilot (Identity/Null/Shuffled); share logs, seeds, plots
4) Preregister final settings; scale up

**Anchor:** Jeff is considering publishing Zack’s work; collaboration path is active.
