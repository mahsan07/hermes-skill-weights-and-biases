# How Weights & Biases Works

Log ML experiments, run sweeps, manage a model registry, and build W&B dashboards.

![Detailed systems blueprint for Weights & Biases](../assets/system-blueprint.png)

## Stages

### 1. Define project run names and config

**Primary surface:** `Training script`

Record the input, operation, observable output, and any decision that changes scope. Stop here if the output is missing, contradictory, or insufficient for the next stage.
### 2. Instrument metrics tables and artifacts

**Primary surface:** `Run metrics and artifacts`

Record the input, operation, observable output, and any decision that changes scope. Stop here if the output is missing, contradictory, or insufficient for the next stage.
### 3. Launch a bounded tracked experiment

**Primary surface:** `W&B tracking server`

Record the input, operation, observable output, and any decision that changes scope. Stop here if the output is missing, contradictory, or insufficient for the next stage.
### 4. Compare runs or execute a sweep

**Primary surface:** `Sweep or registry`

Record the input, operation, observable output, and any decision that changes scope. Stop here if the output is missing, contradictory, or insufficient for the next stage.
### 5. Promote only validated model versions

**Primary surface:** `Experiment dashboard`

Record the input, operation, observable output, and any decision that changes scope. Stop here if the output is missing, contradictory, or insufficient for the next stage.
### 6. Verify dashboard and artifact lineage

**Primary surface:** `Experiment dashboard`

Record the input, operation, observable output, and any decision that changes scope. Stop here if the output is missing, contradictory, or insufficient for the next stage.

## Failure handling

- **Authorization failure:** do not probe credentials or broaden access; report the missing authority.
- **Target ambiguity:** stop before mutation and request the minimum identifying information.
- **Tool or service failure:** retain error evidence, retry only safe transient failures, and cap retries.
- **Verification failure:** classify the run as incomplete even when the preceding operation returned success.

## Completion evidence

The handoff should contain the original request, inspection state, preview or plan, exact execution result, direct verification, and a final receipt naming limitations and withheld actions.
