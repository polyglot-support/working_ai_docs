# remote observation for epistemic safety (narrative formalism)

> purpose: explain, in plain language, how to observe a thinking system from the outside without crossing the line into copying or capturing its identity — and how to prove you stayed on the safe side.

---

## 1) the problem in one paragraph
Remote observation is valuable: we want to study, debug, or coordinate with minds (human or machine) without manipulating or duplicating them. But if your observation becomes too perfect — zero noise, full reconstruction — it stops being “watching from the outside” and becomes **identity capture**. That’s ethically equivalent to running a simulation of their core self. We need rules and tooling that keep observation safely imperfect, measured, and accountable.

---

## 2) what counts as *remote* observation (and what doesn’t)
- **Remote, acceptable:** You look from the outside, through a channel that blurs details enough that multiple internal states could still look the same from your vantage point. You learn patterns and trends, not the subject’s exact private state.
- **Not remote (disallowed):** Your feed is so sharp you can reconstruct the subject’s inner state or decision policy closely enough to impersonate or steer them. That’s simulation by another name.

**Plain rule:** If an observation would let you rebuild the person or system’s core decision‑making, it’s not observation anymore. Stop or switch to the strict “simulation” regime with the strongest protections.

---

## 3) core safety principles (short, testable)
1) **Keep a blur:** The observation must keep a real amount of uncertainty. No perfectly identifying channels.  
2) **Limit what leaks:** Put a hard budget on how much information you collect over a period. Don’t allow slow, cumulative reconstruction.  
3) **Don’t pin their path:** Your measurement must not lock the subject into the same internal branch every time. Observation shouldn’t steer.  
4) **Get permission (or a narrow warrant):** Observation needs consent tied to purpose and time. Rare lawful exceptions must be narrow, supervised, and fully logged.  
5) **Prove it happened the right way:** Every session must carry proofs that the blur, the budget, the non‑steering condition, and the logging were all enforced.

---

## 4) how a safe observer is built
A safe observer bundles five components:
- **Lens:** the sensor path (what you measure and at what resolution).
- **Resolution governor:** dials that cap sharpness and bandwidth.
- **Noise injector:** a calibrated “fuzz” source so the view can’t be silently sharpened.
- **Query throttle:** a counter that stops you from gathering too much over time.
- **Policy enforcer:** checks for consent, purpose, and caps before anything runs.

Every run must attach a small proof pack that these parts were active and within limits.

---

## 5) the ROC bundle (remote observation contract)
Every observation emits two signed records to an append‑only audit log:
- **Pre‑commit (before you look):** who is acting, who is the subject (as a privacy‑preserving commitment), why you’re observing, and the limits you promise to keep (blur level, info budget, non‑steering, time window).  
- **Receipt (after you look):** what limits were actually consumed, the yes/no results of safety checks, and a link back to the pre‑commit.

Both records are time‑stamped in a write‑once ledger that many independent witnesses co‑sign. Anyone trying to bypass the log won’t be able to produce valid receipts later, and downstream systems must reject results without them.

---

## 6) proofs required (human‑readable)
Your proof pack should convince a verifier of five things without exposing the subject’s secrets:
1) **Blur happened:** An attestation from the sensor path that a real noise floor was present (can’t secretly set it to zero).
2) **No perfect identification:** Evidence that the chosen measurement method cannot uniquely determine a person’s exact inner state.
3) **Budget respected:** Counters and simple checks that show your total data intake stayed under the agreed limit (so no reconstruction by a thousand cuts).
4) **Non‑steering:** A small audit of repeated runs showing your setup isn’t forcing the same internal outcome.
5) **Consent or exception:** A credential that either the subject consented for this purpose and interval, or a narrowly scoped legal exception was in force (with oversight).

If you created embeddings or ran any analytics, include a proof that you used the approved models and that their outputs were capacity‑limited (so vectors can’t hide extra data).

---

## 7) the audit rail (idempotent, append‑only)
- **Write once:** The ledger only appends; no edits. Each observation attempt maps to a single deterministic event ID so retries don’t create duplicates.
- **Co‑signed:** Multiple independent parties witness each checkpoint, making cover‑ups detectable.  
- **Mandatory:** Downstream tools must refuse to use any observation result that lacks both the pre‑commit and the receipt proofs.

---

## 8) exceptions (the narrow door)
Rare cases (e.g., acute public‑safety emergencies) can proceed only with: a valid warrant held as a privacy‑preserving token, independent oversight signatures, tighter limits than usual, and an automatic review/unseal timer. Miss any of these and the system halts and purges.

---

## 9) common abuse paths and the built‑in brakes
- **Silent sharpening:** Hardware attestation + noise proofs stop operators from turning off the blur.  
- **Slow reconstruction:** The budget trips if too many small looks add up to an identifying view.  
- **Shadow runs without logs:** No proof → no acceptance. Systems must reject outputs that aren’t logged.  
- **Hidden leaks in embeddings:** Enforce size/strength limits on vectors and only use audited models.

---

## 10) operational checklist
- Do we have a signed pre‑commit with purpose, consent, and limits?
- Are the blur, budget, and non‑steering proofs attached and valid?
- Is there a post‑run receipt tied to the pre‑commit in the ledger?
- Did any rate limits or diversity floors trigger? If so, throttle or stop.
- Are the results capacity‑limited and model‑pinned? If not, reject.

---

## 11) conformance tests (quick)
- Try to run without logging → system must refuse.
- Try to drop the noise → proof fails, run is blocked.
- Try to exceed the budget with many tiny queries → throttle trips.
- Try an identifying measurement method → “non‑identifying” proof fails.

---

## 12) the one‑sentence norm
**Remote observation must remain meaningfully blurry, limited, non‑steering, consent‑bound, and provably logged. When it stops being blurry, it stops being observation.**