---
globs: ["pine/libraries/*.pine"]
---

# Library Files — READ ONLY

Reference implementations. NEVER modify without explicit user request.
These are imported by all indicators and strategies.

## Import Mapping
<!-- TODO: Fill in your library import aliases -->
<!-- Example: -->
<!-- - `lib = your_library` — description of what it provides -->

## Key Rules

1. **READ ONLY** — Never modify library files without explicit confirmation. They are shared across all published indicators.
2. **Verify constraints by reading source** — grep the actual function implementation, don't assume return value ranges.
3. **Import aliases must match** — If a library is imported as `lib`, always call it as `lib.function_name()`.
4. **Check return value ranges before using** — A function returning [0,1] used as [0,100] silently breaks math.
