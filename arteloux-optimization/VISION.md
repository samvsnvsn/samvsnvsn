# Arteloux Optimization — Vision

## Core idea

An online material-layout optimization service for small businesses, workshops,
makers and manufacturers that cut physical materials but do not want, or cannot
justify, expensive industrial nesting/CAD/CAM software.

The customer problem is simple:

> "I have these shapes, this quantity and this piece/sheet/roll of material.
> Arrange them as efficiently as possible so I waste less material."

The product is **not** limited to SigmaNEST, metal cutting, plasma or oxyfuel.

## Materials in scope (potential)

- steel and other metals
- leather
- fabric/textiles
- plastic/acrylic
- wood/sheet material
- foam
- rubber/gaskets
- vinyl
- packaging materials
- composites
- other sheet or irregular materials

## Cutting processes in scope (potential)

- laser
- plasma
- oxyfuel
- waterjet
- CNC router
- knife cutter
- oscillating knife
- plotter
- other 2D cutting processes

## What we sell

Material savings and optimized output, not a CAD/CAM application.

Central sales proposition:

> Do not buy expensive nesting software if you only need the optimized result.

## Strategic principle

Avoid competing with SigmaNEST, ProNest, Lantek and similar suites
feature-for-feature. Arteloux should initially solve a much simpler problem
exceptionally well:

> Give us your parts and material. We find an efficient layout.

Target customers who do not need, or cannot justify, a large industrial CAD/CAM suite.
The experience must be extremely simple. Customers should not need CAM expertise.

## Potential differentiator: irregular material

Support for irregular stock (metal remnants, leather hides, fabric remnants,
irregular foam/rubber/plastic) with marked no-go/defect zones may become an
important differentiator. See PRODUCT-ARCHITECTURE.md.

## Relationship to SOUP

SOUP (Nesting Expert) is an existing asset containing substantial work on real
nesting geometry, production strategy, irregular remnants, clearance, multi-head
constraints, gas/plasma rules, placement optimization, real production examples
and physically cut benchmark nests.

SOUP was built around a specific industrial environment. We must determine which
components are genuinely reusable as a universal geometry/optimization engine and
which are Sigma/metal/process-specific. Do not discard SOUP. Do not blindly rename
it. Audit first.

## What this project is not (yet)

- Not an implementation. Documentation only until the audit, market research and
  MVP definition are complete.
- Not a priced product. Pricing requires market research.
- Not a universal machine-output tool. See the safety boundary in
  PRODUCT-ARCHITECTURE.md.
