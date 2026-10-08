# Arteloux Optimization — Research Questions

These must be answered, in roughly this order, before an implementation roadmap
is written. Answers should be recorded alongside these documents.

## 1. SOUP audit (reusable technology)

- Which SOUP components are genuinely universal geometry/optimization
  (import/normalization, polygon representation, collision detection, placement
  optimization, utilization calculation, irregular remnant handling)?
- Which are Sigma/metal/process-specific (multi-head constraints, gas/plasma
  rules, SigmaNEST-specific formats, thickness-driven clearance)?
- Which could be generalized with moderate effort, and what would that cost?
- What are SOUP's dependencies, licensing constraints and coupling to the
  production environment?
- Which benchmark nests and production examples can serve as test fixtures for
  a universal engine?
- What is the correct migration/reuse strategy: extract, fork, wrap, or rewrite?

## 2. Market and competitors

- Who currently serves small-business nesting (online nesting tools, CAD plug-ins,
  open-source nesters, free tiers of industrial suites)?
- What do they cost, what inputs/outputs do they support, and where do they fall
  short for small customers?
- Is "optimization as a service" already offered? By whom, at what price, and
  with what uptake?
- What quality level (utilization, speed, geometry fidelity) is the realistic bar
  to clear?

## 3. Underserved customer segments

- Which material/process combinations have the weakest existing tooling
  (leather, textiles, foam, gaskets, vinyl, packaging, small-shop metal)?
- For each candidate segment: how do they cut today, what files do they have,
  how much material do they waste, and what is that waste worth?
- Which segments have irregular stock as a routine problem, and how do they
  handle defects today?
- Where do these customers look for solutions, so that outreach can be
  relevant rather than spam?

## 4. Smallest commercially testable MVP

- Which single material/process and input/output pair gives the fastest
  credible test (e.g. DXF/SVG in, nested DXF/SVG + PDF out, rectangular stock)?
- What is the minimum website flow needed to run the proof-before-purchase
  journey end to end?
- Can the MVP be validated with manual or semi-manual fulfilment before the
  engine is fully automated?
- What result metrics must be shown for a customer to trust the preview?

## 5. Commercial model and pricing

- Which model (per optimization, per package, credits, subscription, API) fits
  the identified segment best?
- What price points do customers compare against (software licences, scrap
  cost, outsourced programming)?
- What anti-abuse mechanism keeps the free preview useful without replacing the
  paid output (watermarking, resolution limits, delayed delivery, account
  limits, other)?

## 6. Safety and output

- Which machine/controller families, if any, are worth a validated
  postprocessor early, and how would validation be done?
- How is machine-ready output clearly separated from universal geometry output
  in the product and in customer communication?
- What verification or disclaimer is required before any machine-ready file is
  delivered?

## 7. Acquisition layer

- Which sources of leads are legitimate and permitted for the target segments?
- What qualification criteria separate a genuine prospect from noise?
- What communication channel and consent model does AgentMail need to support?
- CNC intake (a prospect sends only the posted program): which post dialects
  beyond ESSI (ProCut / SigmaNEST) occur in the target segments, and what does
  each one hide (kerf already applied to the path, absolute vs incremental
  moves, multi-torch copies, datum corner)? What minimum the prospect must
  confirm (thickness, material, plate size and shape) before a before / after
  comparison is fair?
- When is a machine-ready return (a post mirroring the prospect's own dialect,
  verified by reading it back) worth more than the geometry package, and what
  supervised cut test closes that loop?
