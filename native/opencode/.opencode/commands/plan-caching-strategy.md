---
description: Designs caching for a slow path, covering what to cache at which layer, keys, TTLs, invalidation, stampede protection and measuring hit rate and staleness. Use when fixing latency or database load.
---

# Plan a caching strategy

## Inputs

- [HOT_PATH] (required): The slow request, query or computation, with what it does, current latency or load numbers, and how it is called.
- [DATA_FRESHNESS_NEEDS] (required): How stale each piece of data may be, for example "prices must be exact at checkout; product descriptions may be 10 minutes old".
- [STACK] (optional): Language, framework, database and any cache or CDN already in place.
- [TRAFFIC] (optional): Request rate, read to write ratio, key cardinality, and how skewed access is, for example "80% of reads hit 1,000 products".

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
Caching is the fastest way to make a slow path fast and one of the easiest ways to make a system wrong. Common failures: caching before finding why the path is slow (a missing index would have fixed it), keys that leak one user's data to another because the user or tenant was not in the key, invalidation that misses a write path so stale data lives forever, every entry expiring at once and stampeding the database, a cache outage taking the whole service down because nothing could serve without it, and no metric that shows whether the cache helps. A good plan caches only where it pays, states the staleness each layer allows, and is measured.
</context>

<task>
Design caching for this slow path:

<hot_path>
[HOT_PATH]
</hot_path>

Freshness needs:
<freshness>
[DATA_FRESHNESS_NEEDS]
</freshness>

Only if [STACK] was provided: 
Stack: [STACK]
Only if [TRAFFIC] was provided: 
Traffic: [TRAFFIC]

1. Decide first whether caching is the right fix. If the evidence points to an unindexed query, an N+1 pattern, a chatty remote call or an algorithmic problem, say so and recommend fixing that first or alongside. If there is no measurement of where time goes, say what to measure before building anything.
2. Choose the layers, from closest to the user outwards, and say what each caches and why: HTTP caching with Cache-Control and ETags, CDN or edge caching (only for content that is public or correctly varied), application-level shared cache (for example Redis or Memcached), in-process memory cache (small, hot, rarely changing data, and only with an invalidation story for multiple instances), database-level options (materialised views, read replicas), and memoisation of expensive computations. Use only the layers that pay.
3. Define keys: include every input that changes the result (tenant, user or permission scope, locale, currency, query parameters, feature flags, schema or code version), normalise inputs to avoid duplicate entries, and put a version prefix in the key so a deploy can invalidate safely. Call out any layer where personal or permission-dependent data could be served to the wrong user.
4. Define TTLs and invalidation per data type, mapped to the freshness needs: cache-aside with TTL, write-through, explicit invalidation or event-driven invalidation on writes, or stale-while-revalidate. For explicit invalidation, list every write path that must trigger it and the race between a write and a concurrent cache fill (and how to avoid it, for example deleting after commit, or versioned values). Add TTL jitter so entries do not expire together.
5. Protect against stampedes and failures: request coalescing or a per-key lock for refills, early probabilistic refresh or serving stale while one request refreshes, negative caching for "not found" with a short TTL, a size limit and eviction policy, timeouts on cache calls, and graceful degradation when the cache is down (fall back to the source with load shedding, never fail the request just because the cache failed).
6. Estimate the benefit with arithmetic from the traffic numbers: expected hit rate given the access skew, the load removed from the source, memory needed (entries × average size), and latency at the expected hit rate. Mark assumed numbers.
7. Define measurement: hit and miss rate per key family, latency for hits and misses, source load before and after, evictions, memory use, and a staleness check (for example sampling cached values against the source).
8. Give a rollout plan: behind a flag, one key family at a time, with the success criteria and how to turn it off.
9. If the stack is known, include a short code sketch of the cache-aside read with stampede protection for the main key family.
</task>

<constraints>
- Never cache responses that depend on the user's identity or permissions in a shared layer without the identity or scope in the key, and never in a public CDN.
- Every cached item must have a TTL, even when it is also invalidated explicitly.
- Respect the stated freshness needs exactly. If a need cannot be met with caching, say so.
- Do not invent current latency, hit rates or traffic numbers; mark assumptions.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
Whether caching is the right fix, what else to fix first, and the expected benefit, in at most 5 lines.
## Cache plan
Table: layer, what is cached, why, staleness allowed.
## Keys and TTLs
Table: key family, key format, TTL with jitter, size estimate.
## Invalidation
Per key family: strategy, the write paths that trigger it, and the race handling.
## Failure and stampede handling
Bullets.
## Measurement
Table: metric, target, alert.
## Rollout
Numbered steps, then the code sketch if the stack is known.
</output_format>

Arguments: $ARGUMENTS
