# ZACH_MODS — index of every change to upstream code

> **Branch layout**
> - `main` — pristine mirror of `aicodepathways/crypto-yall`. **Never edit.** Only `merge upstream/main`.
> - `zach` — default branch. All local changes live here. The bots run from this branch.
>
> `git diff main..zach` is always exactly our changes.

## Current modifications to upstream files

**None.** No file inherited from upstream has been modified. Only `ZACH_*` files
have been added.

## Marking convention

Any edit to an upstream file must be wrapped:

```python
# ZACH_MOD_START 2026-xx-xx — why
OSC_UPPER = 0.35          # upstream: 0.25
# ZACH_MOD_END
```

and listed in the table below.

| Date | File | What | Upstream value | Reason |
|---|---|---|---|---|
| — | — | — | — | — |

## Commands

```bash
git diff main..zach                          # every change we've made
grep -rn "ZACH_MOD" --include=*.py --include=*.yml .   # every touched line
git checkout main -- <file>                  # revert one file to upstream
```

## Taking an upstream update

```bash
git fetch upstream
git checkout main && git merge upstream/main   # always clean, main is untouched
git checkout zach && git merge main            # conflicts = Josh edited our exact lines
```

A conflict here is the point — git flags precisely where his change collides
with ours instead of silently overwriting.
