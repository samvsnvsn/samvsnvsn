# Arteloux Optimization — Product Architecture

Long-term target. Nothing here is implemented. Component boundaries are the
important part; implementation details are deliberately left open.

## Overview

```
Arteloux Website  ──►  Arteloux Engine  ──►  Output Profile
 (customer-facing)      (optimization)        (files/results)
          │                   ▲
          │                   │
          └──── Material/Process Profile
```

## 1. Arteloux Website (customer-facing product)

Uses the existing Arteloux domain/brand infrastructure.

A visitor should be able to:

1. See clear real examples of inefficient vs optimized layouts.
2. Understand potential material savings.
3. Select material/process.
4. Enter material dimensions/thickness where relevant.
5. Upload part files.
6. Set quantities.
7. Request optimization.
8. Receive a visual optimized layout.
9. See utilization/waste statistics and potentially estimated savings.
10. Download appropriate production/output files when available.

The experience must be extremely simple. No CAM expertise required.

**Initial inputs (potential):** DXF, SVG.
Other CAD/vector formats may follow where technically justified.

**Outputs (potential):**

- optimized/nested DXF
- optimized/nested SVG
- PDF/PNG layout
- placement/coordinate data
- machine-specific CNC/G-code, **only** for explicitly supported and validated
  machine profiles/postprocessors

Do not assume ".cnc" is universal. Machine-ready output is separated from
universal geometry output (see section 5).

## 2. Arteloux Engine

To be extracted/adapted from reusable parts of the existing SOUP Nesting Expert
where technically appropriate, after an audit. Conceptual responsibilities:

- geometry import/normalization
- polygon/profile representation
- collision detection
- clearance rules
- nesting/placement optimization
- irregular stock/remnant support
- no-go/defect zones
- utilization calculation
- optimization scoring

The Engine must be material- and process-agnostic. Material/process knowledge
enters through profiles, not hard-coded assumptions.

## 3. Material/Process Profile

Describes the job's material and cutting technology:

- material
- thickness
- cutting technology
- required clearance
- rotation constraints
- grain/direction constraints
- heat/process constraints where relevant
- other process-specific rules

**Rule:** do not hard-code the assumption that thickness alone determines
clearance. Thickness can influence clearance, but material and cutting process
can also matter.

## 4. Output Profile

Translates an Engine result into deliverables:

- DXF
- SVG
- PDF/PNG
- placement data
- machine-specific adapters/postprocessors

## 5. Universal geometry output vs machine-ready output

These are different products.

| Universal geometry output | Machine-ready production output |
| --- | --- |
| Nested DXF/SVG, PDF/PNG, placement data | CNC/G-code for a specific machine |
| Broadly useful across machines and vendors | Requires a known machine/controller, known process, validated postprocessor, appropriate machine profile, and verification |
| Default deliverable | Only for explicitly supported, validated profiles |

Never claim universal machine compatibility.

## 6. Irregular material optimization

Potential differentiator. Arteloux should eventually support irregular stock:

- metal remnants
- leather hides
- fabric remnants
- irregular foam/rubber/plastic stock

Conceptual model:

```
OUTER BOUNDARY
+ NO-GO / DEFECT ZONES
+ PART GEOMETRY
+ QUANTITIES
```

Example: for leather, defects could be marked and parts nested around them.
Existing SOUP work on irregular remnants may be reusable here.

## 7. Acquisition and communication layer (future)

The existing Earning Automaton may later become the acquisition and
communication layer; AgentMail may later handle customer communication.
See COMMERCIAL-HYPOTHESIS.md. Not part of the core product architecture.

## 7a. CNC intake: proof from the customer's own program

Many prospects cannot export parts or a nest; the only thing they can send is
the program their CAM posted (for ESSI machines a `.cnc` from ProCut /
SigmaNEST). The intake path reads that program back into geometry: each cut
contour without its lead-in, holes grouped into parts, identical parts
counted (mirror images kept apart), the plate inferred from the datum and the
cut extents, the process from the tool codes. The same parts are then nested
by the engine and the result is compared with the nest as cut (occupied
extent, largest free rectangle, cut length, pierces). What the program cannot
tell (thickness, material, kerf, the real plate shape, torch copies) is asked
for, never guessed. The deliverable back to the prospect is geometry (the
package) for their own CAM; a machine program is written only under the
section 5 rule, and a post that mirrors the prospect's own dialect is the
candidate for the first validated machine-ready output.

Reference implementation: `arteloux recover-nest` in the private Arteloux
repository (2026-10-08).

## 8. SOUP reuse boundary

Keep Arteloux Optimization separate from the production SOUP repository until
the audit determines the correct migration/reuse strategy. The audit must
classify each SOUP component as:

- genuinely reusable as universal geometry/optimization, or
- Sigma/metal/process-specific, or
- reusable only after generalization.
