# How Weights & Biases Works

The visuals on this page are static SVGs, so they render directly on GitHub on phones and desktop browsers. Each one is generated from a model specific to this skill.

## System architecture

![Detailed system map for Weights & Biases](../assets/system-map.svg)

### Components

- **1. Training script:** participates in define project run names and config.
- **2. Run metrics and artifacts:** participates in instrument metrics tables and artifacts.
- **3. W&B tracking server:** participates in launch a bounded tracked experiment.
- **4. Sweep or registry:** participates in compare runs or execute a sweep.
- **5. Experiment dashboard:** participates in promote only validated model versions.

## Actor and data sequence

![Actor and data sequence for Weights & Biases](../assets/operation-sequence.svg)

### 1. Define project run names and config

**Primary surface:** `Training script`

Record the concrete input, the operation performed, and the evidence produced at this stage. Continue only when the output is sufficient for the next stage; otherwise preserve the blocker and stop.
### 2. Instrument metrics tables and artifacts

**Primary surface:** `Run metrics and artifacts`

Record the concrete input, the operation performed, and the evidence produced at this stage. Continue only when the output is sufficient for the next stage; otherwise preserve the blocker and stop.
### 3. Launch a bounded tracked experiment

**Primary surface:** `W&B tracking server`

Record the concrete input, the operation performed, and the evidence produced at this stage. Continue only when the output is sufficient for the next stage; otherwise preserve the blocker and stop.
### 4. Compare runs or execute a sweep

**Primary surface:** `Sweep or registry`

Record the concrete input, the operation performed, and the evidence produced at this stage. Continue only when the output is sufficient for the next stage; otherwise preserve the blocker and stop.
### 5. Promote only validated model versions

**Primary surface:** `Experiment dashboard`

Record the concrete input, the operation performed, and the evidence produced at this stage. Continue only when the output is sufficient for the next stage; otherwise preserve the blocker and stop.
### 6. Verify dashboard and artifact lineage

**Primary surface:** `Training script`

Record the concrete input, the operation performed, and the evidence produced at this stage. Continue only when the output is sufficient for the next stage; otherwise preserve the blocker and stop.

## Example output shape

![Illustrative output for Weights & Biases](../assets/example-output.svg)

The example is a visual contract: a real run may look different, but it should expose comparable state, provenance, and verification information. It is not presented as evidence of a live external action.

## Decision and stop conditions

![Decision guide for Weights & Biases](../assets/decision-guide.svg)

The workflow stops when the target is ambiguous, the relevant surface is unavailable or unauthorized, or the final artifact cannot be checked. A logged-in session or successful tool call is not by itself proof that the requested outcome is complete.

## Verification checklist

- Confirm every component shown in the system map exists in the target environment.
- Trace the actor sequence using actual tool output or artifact state.
- Compare the result with the example-output information contract.
- Re-read or reopen the final artifact instead of trusting an attempt message.
- Report omitted stages, unsupported capabilities, and remaining human decisions.
