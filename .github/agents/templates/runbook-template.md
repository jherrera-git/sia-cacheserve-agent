# NN – <Category> Execution Runbook (Internal)

## Environment

| Role | Host | Notes |
|---|---|---|
| Resolver / CacheServe | `<RESOLVER_HOST>` | |
| Client A (attack/load) | `<CLIENT_A>` | |
| Client B (availability check) | `<CLIENT_B>` | |
| Management / portal | `<MGMT_HOST>` | |

Tools verified: `dig` / `curl` / `openssl` / `tcpdump` / others: ______

## Baseline (captured before any change)

```
nom-tell -j cacheserve server.get            > baseline/server.json
nom-tell -j cacheserve binding.list layer="*" > baseline/binding.json
```

Baseline file locations / checksums: ______

---

## <TEST-ID>: <Title>

- **Priority:** 
- **Safety tier:** Pass 1 / Pass 2 / Pass 3
- **Evidence Reference:** EV-<TEST-ID>
- **Objective:** 
- **Preconditions / approvals:** 

### Procedure

```
<command>
```

### Raw result

```
<output>
```

### Corrections to docs / build-specific findings

- 

### Rollback (Pass 2/3 only)

```
<commands, in dependency order: unbind consumers first>
```

Rollback verification (diff vs. baseline): ______

### Status

PASS / FAIL / DEFERRED (external dependency: ______)

---

## Master status table (mirror in README.md)

| Test ID | Runbook | Category | Priority | Status | Summary |
|---|---|---|---|---|---|
| | | | | | |
