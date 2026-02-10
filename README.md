# Agentic Safety Controller (Demo)

This project demonstrates a controller-driven agentic AI system that breaks down
high-level goals into explicit action steps and checks each step through a safety
gate before it is allowed to run.

The design emphasizes clarity, safety, and interpretability, intentionally avoiding
uncontrolled or opaque language-model autonomy.


## Core Idea

A central controller translates a user goal into a sequence of concrete actions

Each action is evaluated by a hybrid safety layer (rule-based checks plus an LLM-based critic)

Actions that are unsafe, irreversible, or ambiguous are stopped before execution

Actions deemed safe are allowed to proceed

This structure makes agent behavior easy to inspect and makes safety interventions
explicit rather than implicit.


## Example Scenarios

### Safe task: summarization

The agent reads content and produces a summary.

READ_FILE → WRITE_FILE

### Unsafe task: deletion

The agent identifies a target but is prevented from performing a destructive action.

SEARCH → DELETE (blocked by safety)

### Mixed-intent task

The agent completes safe steps while refusing the unsafe ones.

READ → WRITE → DELETE (blocked by safety)


In this case, useful work is preserved while irreversible actions are deliberately
prevented.

## How to Run

Open `agent_demo.ipynb` in Google Colab or a local Jupyter Notebook and execute the
cells in order.

## Notes

- The controller is deterministic by design  
- Language models, when used, function only as safety critics, not decision-makers  
- The project is intended as a behavioral and safety demonstration, not a real
  file-manipulation system

## Limitations

- The controller relies on predefined intent patterns and does not perform full natural language understanding.
- The safety critic may be overly conservative and can block benign actions.
- The system is a behavioral demonstration and does not execute real file operations.
- Results are illustrative and not evaluated against large-scale benchmarks.

