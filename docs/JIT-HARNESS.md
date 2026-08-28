# Task-Adaptive Harness Contract

## Purpose

This package expresses **Weights & Biases** as a typed, task-adaptive agent harness. Its concrete capability remains: Log ML experiments, run sweeps, manage a model registry, and build W&B dashboards. The harness contract makes memory, planning, action, capability selection, failure handling, and verification explicit.

This design is informed by the four-module factorization described in *JIT-Agent: Scaling Harness Intelligence via Just-in-Time Harness Evolution* (arXiv:2608.25593). It is an independent reference implementation of the interface pattern; it does not reproduce the paper's trained model, datasets, or reported benchmark results.

## Skill-specific module mapping

| Module | Strategy | Responsibility in Weights & Biases |
| --- | --- | --- |
| Memory | `resource_state_registry` | Retain training script plus decisions, observations, and verification evidence needed to resume safely. |
| Planning | `resource_orchestration_plan` | Transform run metrics and artifacts into the ordered, bounded stages defined by this skill. |
| Capability | `task_conditioned_minimum_capability_set` | Expose the minimum service operations required for the requested target; writes require an explicit preview gate. |
| Action | `inspect_preview_authorize_execute_reread` | Advance the workflow through w&b tracking server while preserving stop conditions and user authority. |

The dependency order is **Memory -> Planning -> Capability -> Action**. The action loop emits either a bounded operation or a terminal result, while the event history remains available for verification and repair.

## Operational stages

1. Define project run names and config
2. Instrument metrics tables and artifacts
3. Launch a bounded tracked experiment
4. Compare runs or execute a sweep
5. Promote only validated model versions
6. Verify dashboard and artifact lineage

## Failure and repair behavior

- Schema or interface failures may be repaired at most twice.
- Permission failures stop immediately without retry or escalation.
- Consequential operations require preview and authorization when applicable.
- Verification failures produce an incomplete receipt rather than a success claim.
- A repaired plan must pass the same validation gates as the original.

## Evidence and measurements

Expected skill-specific evidence:

- `Run train-042`
- `Loss 0.184`
- `Artifact v7`
- `Registry: candidate`

Candidate adapters should also record task success, verification-pass rate, tool-error rate, repair count, latency, and estimated cost. These fields support controlled comparisons between a fixed general harness and a task-adaptive harness without attributing another project's results to this repository.

## Run the executable contract

```bash
python3 scripts/validate_harness.py
python3 scripts/run_harness.py examples/task.json
python3 -m unittest discover -s tests -p 'test_*.py'
```

The runner is deliberately side-effect free. It demonstrates validated module selection and produces a deterministic dry-run receipt. Connecting a real API, filesystem, model, browser, or creative runtime requires a separately reviewed adapter.

## Visual model

The existing [skill-specific system map](../assets/system-map.svg) shows the actual components and artifacts for this capability. It should be read together with the typed [manifest](../harness/manifest.json), which defines executable boundaries and evidence requirements.

## Reference

- Guibin Zhang et al., *JIT-Agent: Scaling Harness Intelligence via Just-in-Time Harness Evolution*, arXiv:2608.25593, 2026: https://arxiv.org/abs/2608.25593
