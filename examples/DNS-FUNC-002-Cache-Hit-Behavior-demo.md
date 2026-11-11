# DNS-FUNC-002 – Cache Hit Behavior (Demo Run)

Example of the agent's runbook format, executed live against a CacheServe lab resolver.

## Environment

| Variable | Value used |
|---|---|
| `RESOLVER_HOST` (SSH) | `<resolver-node>` |
| `RESOLVER_QUERY_IP` | `<resolver-internal-ip>` |
| `RESOLVER_NAME` | `world` (from `resolver.list`) |
| `CACHE_TEST_DOMAIN` | `example.com` |

Tools: `dig`, `/usr/local/nom/sbin/nom-tell` (installed path, not on `$PATH`)

## Classification

- **Safety tier:** Pass 1 (read-only) plus a single-name cache flush. The flush changes cache state only, not configuration, so no baseline or rollback is needed.
- **Priority:** P1
- **Evidence Reference:** EV-DNS-FUNC-002

## Objective

Query the same domain twice and show the second answer is served from cache.

## Procedure and raw results

All steps run on the resolver node.

```bash
N=/usr/local/nom/sbin/nom-tell; D=example.com; R=world
$N cacheserve resolver.list                                    # 1. -> name => 'world'
$N cacheserve resolver.flush name=$R "target=(name $D)"        # 2. start cold
$N cacheserve resolver.statistics name=$R all=true             # 3. baseline
dig @<RESOLVER_QUERY_IP> $D A +time=2 +tries=1                 # 4. first query
$N cacheserve resolver.inspect name=$R domain=$D               # 5. confirm cached
$N cacheserve resolver.statistics name=$R all=true             # 6. counters
dig @<RESOLVER_QUERY_IP> $D A +time=2 +tries=1                 # 7. second query
$N cacheserve resolver.statistics name=$R all=true             # 8. counters
```

| Step | Query time | TTL | `lookups` | `cache-misses` | `recursive-lookups` | `requests-sent` |
|---|---|---|---|---|---|---|
| 3 baseline | – | – | 7021126 | 714 | 791 | 1032 |
| 4/6 first query (cold) | **561 ms** | 300 | 7021131 | 715 | 792 | 1037 |
| 7/8 second query (warm) | **4 ms** | 298 | 7021132 | 715 | 792 | 1037 |

## Validation

| Criterion | Result |
|---|---|
| Both queries return `NOERROR` with the same answer set | Met (`172.66.147.243`, `104.20.23.154`) |
| Second query materially faster | Met: 561 ms to 4 ms |
| Domain present in cache after first query (`resolver.inspect`) | Met |
| No upstream activity for the second lookup | Met: `cache-misses`, `recursive-lookups` and `requests-sent` unchanged; only `lookups` +1 |

The TTL falling from 300 to 298 also shows the answer came from the cache.

## Findings

- The first query's counters rose by more than one lookup (+5 `lookups`, +5 `requests-sent`). One cold lookup triggers extra internal lookups, such as NS/glue resolution. The pass criterion is the delta between the first and second query, not the absolute numbers.
- Cache hits = `lookups` − `cache-misses` (per the Command Reference).
- Counters are ground truth; query time alone can be skewed by network jitter.

## Status

**PASS**

## Cleanup

None required. Optionally flush the name again with the step 2 command.
