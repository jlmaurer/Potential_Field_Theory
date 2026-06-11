# Lab Framework: Geophys 5142 Potential Field Theory

## Design Philosophy

Labs are designed around **scaffolded productive struggle**: students should wrestle
meaningfully with the physics and algorithms, but not lose hours to syntax errors or
missing context. The goal is that a prepared student finishes in ~2–3 hours; an
unprepared one finishes in ~4 hours with more reflection.

Each lab has three tiers of tasks that decrease in scaffolding:

| Tier | Name | Structure | Purpose |
|------|------|-----------|---------|
| 1 | **Guided** | Signature + docstring + partial code skeleton | Remove syntax barriers; focus on physics |
| 2 | **Supported** | Signature + docstring + hints available on request | Independent implementation with safety net |
| 3 | **Open** | Problem statement only | Genuine synthesis and design choices |

Written response cells appear throughout — these are not optional and cannot be
answered by running code alone.

---

## Cell Taxonomy

Every cell is tagged in its first line so students instantly know what to do with it.

### Code cells

```python
# [PROVIDED] ─────────────────────────────────────────────────────────────────
# Run this cell as-is. Do not modify it.
```

```python
# [IMPLEMENT] ────────────────────────────────────────────────────────────────
# Complete the function below. Replace each `raise NotImplementedError` with
# correct code. Read the docstring carefully before writing anything.
```

```python
# [VALIDATE] ─────────────────────────────────────────────────────────────────
# Run this cell to check your implementation. A passing result prints ✓ PASS.
# A failing result prints the expected vs. actual values to help you debug.
# Do not modify this cell.
```

```python
# [EXPLORE] ──────────────────────────────────────────────────────────────────
# This cell is a starting point. Modify it freely to answer the question above.
```

### Markdown cells (written responses)

Each question requiring a written answer ends with:

```markdown
**Your response:**

> *(Write 3–5 sentences here. Replace this line.)*
```

Students should write directly in the notebook in that cell.

---

## Hint System

Each lab defines a `hints` dictionary near the top in a `[PROVIDED]` cell.
Students access hints explicitly — they don't appear by default.

```python
# Access a hint by key, e.g.:
print(hints['p1_sphere_outside'])
```

Hints give physical intuition or point to a specific equation — they do **not**
give code. A hint might say:

> "Outside a uniform sphere, all the mass behaves as if concentrated at the
>  center. See Blakely eq. 3.4. What does r represent in that limit?"

If a student uses a hint, encourage them to note it in their written response.

**Convention for hint keys:** `p{part}_{short_descriptor}`
  e.g., `p1_sphere_outside`, `p2_bouguer_density`, `p3_prem_shells`

---

## Validation Cell Design

Validation cells use absolute and relative tolerances appropriate for the problem.
They test at least two cases: a trivial/degenerate case and a physically meaningful one.

```python
# [VALIDATE] ─────────────────────────────────────────────────────────────────
import numpy as np

def _check(label, got, expected, rtol=1e-4):
    if np.allclose(got, expected, rtol=rtol):
        print(f"  ✓ PASS  {label}")
    else:
        print(f"  ✗ FAIL  {label}")
        print(f"    expected: {expected}")
        print(f"    got:      {got}")

_check("sphere potential at r=2R", sphere_potential(2*R, rho, R), <expected_value>)
_check("sphere potential at r→∞ → 0", sphere_potential(1e9, rho, R), 0.0, rtol=1e-3)
```

---

## Difficulty Calibration Per Lab

| Lab | Primary difficulty driver | Tier 1 | Tier 2 | Tier 3 |
|-----|--------------------------|--------|--------|--------|
| 0   | Environment / syntax     | Setup, NumPy basics | Simple vector ops | Custom visualization |
| 1   | Numerical methods        | FD stencil | BC implementation | Convergence analysis |
| 2   | Physics (gravity)        | Sphere/plate formulas | PREM integration | Profile interpretation |
| 3   | Physics (magnetics)      | Dipole field | IGRF evaluation | Anomaly identification |
| 4   | Math (spherical harmonics)| Legendre recursion | Synthesis/analysis | Power spectrum |
| 5   | Algorithms (inv. problems)| Talwani polygon | G-matrix construction | Regularization choice |
| 6   | Signal processing (FFT)  | 1-D transforms | 2-D upward cont. | Filter design |
| 6.5 | Numerical stability      | Stable upward cont. | Downward cont. | Noise sensitivity |

---

## Time Budget (target ~2.5 hours for a prepared student)

| Section | Target time |
|---------|-------------|
| Background reading + setup | 10 min |
| Part 1 (Guided, Tier 1) | 40 min |
| Part 2 (Supported, Tier 2) | 50 min |
| Part 3 (Open, Tier 3) | 40 min |
| Synthesis questions (written) | 20 min |
| Extensions (optional) | open |

If a student is still on Part 1 after 60 minutes, that is a signal to the
instructor — not an invitation to make Part 1 easier.

---

## Assessment Rubric (30% of course grade, per-lab)

| Category | Points | What earns full credit |
|----------|--------|------------------------|
| Correctness (Tiers 1–2) | 40 | Validation cells pass; numerical results match expected ranges |
| Analysis & interpretation | 30 | Written responses show physical reasoning, not just restating output |
| Visualization | 15 | Axes labeled with units; colorbar where appropriate; informative title |
| Open-ended (Tier 3) | 15 | Thoughtful design choices explained; results discussed |

**Note on partial credit:** A function that fails the validation test but has a
correct approach (wrong sign convention, off-by-one index) earns ~60% of that
item's points if the student explains the discrepancy.

---

## Building a New Lab: Checklist

When creating a new lab from `lab_template.ipynb`:

- [ ] Fill in header metadata (module, estimated time, prerequisites)
- [ ] List 3–5 specific learning outcomes (measurable verbs: compute, implement, compare, explain)
- [ ] Write the `hints` dict before writing any `[IMPLEMENT]` cell
- [ ] For every `[IMPLEMENT]` cell: write docstring first, then skeleton, then validation
- [ ] Ensure at least one plot per Part (labeled axes, units)
- [ ] Include at least 2 written-response questions per Part
- [ ] Include at least one "why does this make physical sense?" question in Synthesis
- [ ] Add 1–2 Extensions that are genuinely harder (not just "do the same thing again")
- [ ] Test the lab end-to-end with a correct solution before distributing
- [ ] Verify all `[VALIDATE]` cells pass against your reference solution

---

## File Naming Convention

```
labs/
  M{n}/
    lab{n}.ipynb          ← student version (stubs, no answers)
    lab{n}_solution.ipynb ← instructor solution (not distributed)
    data/                 ← any data files specific to this lab
```

The student version should be self-contained: all data is either generated in
a `[PROVIDED]` cell or loaded from `data/` with a relative path.
