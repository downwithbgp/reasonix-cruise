---
name: prop-test
description: Generate property-based tests to find invariants and edge cases that unit tests miss.
---

# Property-Based Test Generation

Generate and run property-based tests that discover edge cases unit tests miss. Find invariants in code, express them as properties, then verify across random inputs.

## Process

### 1. Identify the target
Read the function/module the user points at (or ask if unspecified). Understand:
- Input domain (types, ranges, constraints)
- Output domain
- Side effects
- Assumptions baked into the code

### 2. Discover invariants
Ask these questions about the code:
- **Roundtrip:** `decode(encode(x)) == x` — serialization, conversion
- **Idempotence:** `f(f(x)) == f(x)` — normalization, cleanup
- **Monotonicity:** if `a > b` then `f(a) >= f(b)` — scoring, sorting
- **Commutativity:** `f(a, b) == f(b, a)` — symmetric operations
- **Associativity:** `f(f(a, b), c) == f(a, f(b, c))` — combining
- **No-op boundary:** `f(empty_input) == empty_output` — edge case handling
- **Involution:** `f(f(x)) == x` — negation, reverse, complement
- **Conservation:** sum/count of inputs equals sum/count of outputs
- **Uniqueness:** generated IDs/keys never collide
- **Determinism:** same input always produces same output

State which invariants you think hold and why. If unsure, ask.

### 3. Write property tests
Pick the right framework for the project's language:

| Language | Framework |
|----------|-----------|
| Rust | `proptest` (preferred) or `quickcheck` |
| Python | `hypothesis` |
| TypeScript/JS | `fast-check` |
| Go | `rapid` or `gopter` |
| Java/Kotlin | `jqwik` |
| C# | `FsCheck` |
| Haskell | `QuickCheck` |
| OCaml | `qcheck` |

For Rust specifically:
```rust
use proptest::prelude::*;

proptest! {
    #[test]
    fn prop_roundtrip_encode_decode(data in any::<Vec<u8>>()) {
        assert_eq!(data, decode(&encode(&data)).unwrap());
    }
}
```

### 4. Run and iterate
Run the tests. Property tests shrink on failure to find minimal counterexamples.
- If a property fails: the code has a bug (fix it) OR the invariant didn't hold (rethink it)
- If all pass: report coverage — which invariants hold, which you couldn't express
- If generation is too slow: narrow the input domain with strategy filters

### 5. Report
Summarize:
- How many invariants tested
- Which passed / failed
- Any bugs found
- Any invariants you wanted to test but couldn't (domain too complex, framework limitation)

## Guardrails
- Don't rewrite the function under test unless a property proves it's wrong
- Don't add `proptest`/`quickcheck` as a production dependency — dev-dependency only
- For `no_std` crates, use `quickcheck` which works without std (or skip with a note)
- If property tests are too slow for CI, gate them behind a `#[cfg(feature = "property-tests")]` feature flag
