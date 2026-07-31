

<p align="center">
  <img src="images/banner.png" alt="Aizen Samples - Harbor task samples for feature-development coding" width="880">
</p>

<p align="center">
  <strong>Sample Harbor task surface for studying execution-verified feature-development coding environments.</strong>
</p>

<p align="center">
  <a href="#summary"><img alt="Built by Ethara.AI" src="https://img.shields.io/badge/built%20by-Ethara.AI-ee00ee.svg"></a>
  <a href="#sample-purpose"><img alt="Purpose: task inspection" src="https://img.shields.io/badge/purpose-task_inspection-35d0ba.svg"></a>
  <a href="#task-format"><img alt="Format: Harbor" src="https://img.shields.io/badge/format-Harbor-105864.svg"></a>
  <a href="#verification-contract"><img alt="Verifier: executable tests" src="https://img.shields.io/badge/verifier-executable_tests-3776AB.svg"></a>
</p>

<p align="center"><sub>
  <a href="#summary">Summary</a> &middot; <a href="#sample-purpose">Purpose</a> &middot; <a href="#task-format">Format</a> &middot; <a href="#verification-contract">Verification</a> &middot; <a href="#repository-layout">Layout</a> &middot; <a href="#reproduction">Reproduction</a>
</sub></p>

# Aizen Samples

**Aizen Samples is the inspection and demonstration surface for Aizen's feature-development coding
tasks.** It is meant to show how Aizen task bundles are structured, how the agent-facing prompt is
separated from verifier-only assets, and how `FAIL_TO_PASS` / `PASS_TO_PASS` checks define the
reward contract.

The sample repository follows the same conceptual task format as Aizen's production task surface:
containerized repository environments, explicit feature requirements, callable interface contracts,
and hidden executable verifiers.

## Summary

| Property | Description |
| :--- | :--- |
| Project | Aizen Samples |
| Organization | Ethara.AI |
| Parent project | Aizen |
| Domain | Agentic coding for feature-level software development |
| Task type | Code generation inside repository context |
| Language scope | Python, Go, Rust, JavaScript, and TypeScript |
| Format | Harbor task bundle |
| Verifier | Executable tests over target and preservation behavior |
| Intended use | Task inspection, harness integration, and reproduction workflow examples |

## Sample Purpose

The samples repository is designed to make the Aizen task contract easy to inspect:

- What the agent sees in `instruction.md`.
- How the repository environment is built.
- Which metadata belongs in `task.toml`.
- How target tests and preservation tests are represented.
- How verifier-only assets are separated from the agent-visible workspace.
- How a Harbor-compatible harness can run and grade a task.

The goal is clarity for researchers and integration partners: a reader should be able to understand
the task lifecycle without needing private project context.

Aizen's broader task scope covers multi-language software engineering surfaces, including Python,
Go, Rust, JavaScript, and TypeScript repositories.

## Task Format

Each sample task uses the Harbor bundle shape:

```text
dataset/<task-id>/
|-- task.toml                  # task metadata and runtime contract
|-- instruction.md             # prompt presented to the agent
|-- environment/               # containerized repository environment
|   |-- Dockerfile
|   `-- ...
|-- solution/                  # reference patch and oracle helper, verifier-side only
|   |-- fix.patch
|   `-- solve.sh
`-- tests/                     # executable verifier
    |-- test.sh
    `-- ...
```

The task statement should specify the feature behavior and callable interface clearly enough for an
agent to implement it without seeing the hidden verifier.

## Verification Contract

Aizen sample tasks are centered on two test families:

| Check family | Role |
| :--- | :--- |
| `FAIL_TO_PASS` | Tests that define the missing feature and should become passing after implementation. |
| `PASS_TO_PASS` | Tests that protect existing behavior and should remain passing throughout the task. |

A valid sample demonstrates the full transition: the base state preserves non-target behavior while
the target feature fails, and the reference patch makes the verifier pass.

## Metadata Fields

Task metadata should make provenance and execution requirements explicit:

| Field | Meaning |
| :--- | :--- |
| `instance_id` | Stable task id |
| `repo` | Source repository |
| `base_commit` | Starting commit |
| `problem_statement` | Agent-facing task statement |
| `FAIL_TO_PASS` | Target tests |
| `PASS_TO_PASS` | Preservation tests |
| `difficulty_level` | `L1` or `L2` task mode |
| `interface_spec` | Callable interface contract |
| `image_name` | Container image or environment id |
| `repo_settings` | Repository-specific setup metadata |

## Repository Layout

```text
aizen-samples/
|-- README.md
|-- LICENSE
|-- images/
|   `-- banner.png
`-- dataset/
    `-- <task-id>/
        |-- task.toml
        |-- instruction.md
        |-- environment/
        |-- solution/
        `-- tests/
```

## Reproduction

A Harbor-compatible run follows the task-local manifest:

```bash
cd dataset/<task-id>

# Build or start the environment declared by task.toml.

# Give instruction.md to the agent and let it modify the workspace.

# Run the verifier.
bash tests/test.sh
```

`task.toml` is the source of truth for the environment, timeout, agent-visible files, and verifier
command.

## Relationship To Aizen

Aizen is the parent project for feature-development coding environments. This samples repository is
the public task-inspection surface for that work: it presents the bundle layout and verifier
contract in the same Harbor-oriented form expected by downstream harnesses.

## License

Released under the **MIT License**. Individual task bundles may carry additional license and
attribution obligations inherited from their source repositories, environments, and dependencies.
