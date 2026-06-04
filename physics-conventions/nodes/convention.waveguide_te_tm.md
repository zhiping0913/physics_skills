---
skill_id: convention.waveguide_te_tm
type: convention
summary_50t: >
  TE = transverse electric (E_z = 0), TM = transverse magnetic (H_z = 0),
  relative to the propagation direction. Warning: some European/Russian texts
  use the opposite naming convention.
---

# Waveguide TE/TM mode conventions

The TE/TM classification of waveguide modes follows Jackson §8.1 and is the
standard US physics convention. Confusion arises because European and Russian
literature sometimes uses the opposite naming.

## Project standard (Jackson / US physics)

```
TE = Transverse Electric: E_z = 0
TM = Transverse Magnetic: H_z = 0
```

"Transverse" means zero component along the **propagation direction** k̂ (the
z-axis of the waveguide), **not** relative to the interface normal.

## Warning: European / Russian alternatives

Some European and Russian texts define TE as E ⟂ to the **interface** (i.e.,
perpendicular to the conducting wall or dielectric boundary). In waveguide
problems, this is often the **opposite** naming:

```
Russian "TE" → US "TM" (for waveguide problems)
Russian "TM" → US "TE"
```

When reading Russian waveguide texts (e.g., Vainshtein, Katsenelenbaum),
always check the definition in the opening chapter before applying mode
classification.

## Plasma mode naming (separate system)

Plasma wave modes use an entirely different naming system:

```
O-mode: E ∥ B₀    (ordinary mode, field parallel to background B)
X-mode: E ⟂ B₀    (extraordinary mode, field perpendicular to background B)
```

These are **not** equivalent to TE/TM and should not be mapped onto the
waveguide classification. The O/X naming refers to orientation relative to
the background magnetic field, not to propagation.

**References**: Jackson §8.1, Collin (1991) Field Theory of Guided Waves,
Swanson (2003) Plasma Waves.
