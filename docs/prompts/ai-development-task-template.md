# AI Development Task Template

Use this template when creating prompts for AI coding agents or when drafting GitHub Issues.

The goal is to clearly define the task before implementation.

---

## Objective

Describe the goal of the task.

Example:

```
Add lazy loading support to the dataset loader to reduce memory usage when
working with large datasets.
```

---

## Context

Provide relevant context about the repository, system, or feature.

Include:

- background information
- architectural constraints
- related modules or components

Example:

```
The dataset loader currently loads all data eagerly into memory.
Large datasets cause significant memory usage.
Lazy loading should allow datasets to load on demand.
```

---

## Relevant Files

List files or directories likely involved.

Example:

```
dataset_loader.py
dataset.py
tests/test_dataset_loader.py
```

---

## Constraints

Describe any restrictions or requirements.

Examples:

- preserve existing public APIs
- avoid new dependencies
- maintain backward compatibility
- follow existing repository patterns

Example:

```
- Preserve the current dataset API.
- Do not introduce new dependencies.
- Follow existing repository coding patterns.
```

---

## Proposed Approach (Optional)

If helpful, suggest a possible approach.

Example:

```
Replace eager dataset loading with an iterator-based implementation.
Load datasets only when accessed.
```

---

## Acceptance Criteria

Define clear success conditions.

Example:

```
- Existing tests pass
- New tests validate lazy loading behavior
- Memory usage is reduced when loading large datasets
```

---

## Validation

Describe how the change should be verified.

Examples:

- unit tests
- integration tests
- benchmarks
- CI checks

Example:

```
Run existing test suite and add new tests validating lazy loading behavior.
```

---

## Notes for AI Agents

Before implementing:

1. Analyze relevant files
2. Confirm assumptions
3. Produce minimal diffs
4. Maintain repository coding conventions
5. Ensure tests pass
