# Phase 2: Generate References 📚

> 📍 **Phase 2 — Generate References** | Create supporting reference documents.

## references/architecture.md

Generate from the package scan. Include:

- **Repository layout** — directory tree with generated/hand-written annotations (mark `_generated/` clearly; for inline layout, mark header-identified generated files)
- **Namespace layout** — tree under `<namespace-root>/` showing top-level, `models/`, `operations/`, `aio/`, `aio/operations/`
- **Code generation** — toolchain (TypeSpec emitter `@azure-tools/typespec-python` or autorest), `tsp-location.yaml` format and commit pin, or `swagger/README.md` for legacy autorest
- **Generated vs custom** — table showing mechanism, location (`_generated/` directory OR header comment), when to use which
- **Public client types** — all sync/async client classes with file locations and their purpose
- **API version management** — where the version enum lives, how `_patch.py` (if any) interacts with it
- **Key supporting files** — table of important files (policies, helpers, `_serialization.py`, `_vendor.py`, etc.) and their purpose
- **Dependencies** — key runtime deps from `pyproject.toml`/`setup.py` (e.g., `azure-core`, `isodate`, `typing-extensions`) and dev/test deps
- **Build / test / lint commands** — reference the MCP tools or `azpysdk` entry points; do not duplicate commands already in `doc/tool_usage_guide.md`

**Important**: Only include information that is accurate based on scanning the actual code. Mark anything uncertain with `<!-- TODO: Verify -->`.

## references/customizations.md (if any `_patch.py` file is non-empty, or hand-written utility modules exist)

Generate from reading the actual customization files. For each non-empty `_patch.py` and for each hand-written utility module:

- **Problem**: What issue does this customization solve?
- **Solution**: What does it do (override, new method, type wrapping, policy, etc.)?
- **When to update**: What changes in the generated code would break this?
- **Code example**: A short, real snippet extracted from the file (not fabricated).
- **Async counterpart**: For sync-level customizations, the matching file under `aio/` and its parity status.

Also include:
- **Common Python customization patterns** — table (method override, new method, field transformation, `__all__` re-export, custom pipeline policy, credential wrapping, LRO/paging override)
- **Adding a new customization** — pointer to `azsdk_customized_code_update` + the package-specific touchpoints (which `_patch.py`, which `__init__.py` to update, where to add the async mirror)
- **Removing a customization** — how to unwind a patch cleanly (delete in `_patch.py`, remove from `__all__`, remove re-export from `__init__.py`, delete async mirror)
- **Troubleshooting** — silent import failures (missing `__all__` entry), stale references to removed generated symbols, async/sync drift, double re-export conflicts
- **Quick-reference checklist** — post-regeneration verification steps (run `azsdk_package_run_check`, verify async parity, verify public API shape via `__init__.py` diff)

## Step 1 — Present

Print the proposed reference files content.

## Step 2 — CONFIRM

Question: "Create these reference files now (recommended), edit first, or skip?"

📍 **Phase 2 complete** | Created: references/ | Next: Phase 3

---
## → Next: Phase 3 — Validate
Read [03-validate.md](03-validate.md) and begin immediately.
