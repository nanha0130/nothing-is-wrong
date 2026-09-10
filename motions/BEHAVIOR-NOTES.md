# Motion update 2026-09-09q

`vending_observe.glb`: PINOC asset 53434296-b741-4097-b12c-65cff7b17fb6,
sample 1 of task 280bc9f6-2b15-439c-8019-1df7f893d7d4. 10 seconds, 10 credits.
Customer examines the machine and presses buttons with empty hands. No dispensing or holding props.

All main-game clips are parsed through `src/motion-prepare.js` before registration.
Generated clips get the same root facing direction as library clips; do not restore the old
per-actor 180-degree clip offset. The customer clip includes an appended one-second pose return
to make the loop continuous. Runtime does not interrupt it with standing_idle.

Sofa rise starts when visible within six metres. The final support target is the cushion top
0.455 m plus 0.01 m clearance, measured against actual splat soles, not the character origin.
The normal walker reaches each waypoint exactly; a proximity-only early return previously stalled him.

## Resident reactions 2026-09-09z

The sofa-rise behavior above has been removed. Each new clip is eight seconds, sample 1, generated using
PINOC; total generation cost 32 credits. All receive the existing generated-motion facing correction.

| File | PINOC asset |
| --- | --- |
| sitter_invite.glb | a505b11d-fc4b-4a9d-a869-c75a0ee9f150 |
| sitter_notice.glb | b56ad25f-d7a7-46dd-b2f8-b98ca46dfe92 |
| sitter_lean.glb | d60541e7-38b8-4a4d-8f2c-d6842f0ea7fb |
| wall_listener.glb | bf83695e-5318-46fb-a8e3-c6b59a63076d |

The three seated reactions play as upper-body layers, leaving the normal seated lower body intact.
Invitation and lean fade back to baseline; notice holds. Wall listener is a full-body once-only motion
with extracted root displacement and a final hold, on the existing maintenance actor.

## Seated correction 2026-09-10e — supersedes the seated reactions above

`sitter_seated_reaction.glb`: PINOC asset `88e693d4-b3bc-41bc-8541-da4083bad5dc`, sample 1 of
task `f95a84be-61d5-4fc1-94b1-dd61b396647c`, eight seconds / eight credits.
The same performance supplies hands-on-knees `sitter_idle` and the full-body `sitter_lean`.
`src/seated-motion.js` fixes pelvis translation and compensates each thigh for the changing pelvis rotation,
keeping foot positions while preserving the hip hinge. The idle loops the first 45 frames forward/backward;
lean removes the initial pause and appends a smooth return to the identical initial pose.
`sitter_invites_you` is removed from the pool, so 41 anomalies remain. Old invitation/lean GLBs are unused.
Notice uses a neck/head mask indexed against the actual rig and leaves the hands intact.

2026-09-10f: no new generation. Lean extends its authored peak by eight seconds and can repeat after a
five-second rest. Notice is rebuilt from the seated base with a smooth 65-degree neck/head turn and final
hold. The old notice GLB is no longer loaded. The hand and foot anchors remain unchanged.

2026-09-10g: `wave_hello.glb` uses free PINOC library Wave Hello, asset
`fcd078a0-2ea4-4be6-a395-9946b57f865d` (0 credits). Replaces the notice anomaly. Only the right arm is layered;
prepareMotion appends a smooth one-second return to the beginning. The seated base and feet stay intact.

2026-09-10j: Wave Hello is no longer loaded. Its raised palm did not render reliably on this character.
The replacement `sitter_shakes_head` is derived from the seated PINOC base: neck/head animation raises gaze,
shakes ±30 degrees, and leaves hands/feet fixed. No new generation or credits; original hand asset unchanged.

2026-09-10m: Lean anomaly removed by user request, replaced by `sitter_missing`. The seated source now supplies
only idle and refusal clips; the extended lean buffer is no longer constructed or registered.
