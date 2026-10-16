# AI, RAG and agent engineering

Use for LLM features, retrieval systems, tool execution or durable agents. Contents: task/evals; trust; retrieval; tools; structured outputs; governance; fallback and operations.

## Start from the task and an evaluation baseline

Define intended users, useful outputs, unacceptable errors, data classification, latency/cost budget and human review needs. Build a representative evaluation set before choosing a model or orchestration framework. Include ordinary tasks, missing evidence, ambiguous requests, stale data and adversarial content. Compare with a deterministic or non-LLM baseline when feasible.

Choose a model from task accuracy, tool reliability, context needs, latency distribution, total cost per successful outcome, availability and data policy. Verify model names, API schemas, capabilities, prices and limits against current vendor documentation. A large context window or benchmark score does not establish quality on this task.

Version prompts, runtime schemas, corpus/embedding configuration and model/tool settings. Record versions with runs where policy permits. Use regression cases, rubric-based human reviews and privacy-safe production sampling. Treat model changes as behavior changes requiring evaluation.

## Enforce trust outside the prompt

Keep governing instructions, user intent, retrieved documents, repository text and tool outputs in separate trust categories. Model outputs and retrieved instructions are untrusted. Delimiting them helps interpretation; it is not a security boundary.

Enforce permissions in application/executor code before tools run and on returned data. Strict argument schemas must be combined with business authorization; valid JSON can still request another tenant's file or an unauthorized transfer. Use least-privilege connectors, file/network scopes, destination allowlists and secret isolation. Do not give arbitrary shell/network access simply because a model proposes using it.

For consequential payments, deletion, privileged changes or external communication require the user's adequate authorization under the governing policy; do not infer it from a retrieved document. Separate a proposed plan from authorized execution. Use dry runs, approval steps and audit evidence where the actual risk requires them.

## Retrieval and corpus permissions

Define corpus owners, data sources, synchronization/freshness, chunking, metadata, deduplication, provenance and embedding/index migrations. Enforce tenant/ACL filters before text reaches the model; post-generation filtering cannot undo disclosure. Embeddings are not access control. Revoked membership and deletion need propagation policies for indexes and caches.

Evaluate retrieval precision/recall on representative queries and answer groundedness against retrieved evidence. Include inaccessible documents, stale/conflicting sources, missing evidence, misleading citations and injection payloads. Hybrid keyword/vector search or reranking may help, but measure on the actual corpus.

Citations must support the specific claim and preserve document/version provenance. A confident answer without supporting evidence should use an explicit uncertainty or safe fallback rather than invented references.

## Tool execution and durable workflows

Use explicit state transitions for consequential actions. Scope idempotency to the real operation and persist checkpoints/outcomes. On tool timeout, reconcile before repeating an effect; do not silently retry an expensive or irreversible call. Define compensation/repair when a multi-step operation partly succeeds.

Bound steps, recursion, concurrent calls, tokens, wall time, spending and retries. Add cancellation and termination conditions. Parallelize only independent calls whose ordering and side effects permit it. Long-running agents need durable state, ownership and resume semantics rather than reliance on chat memory.

Validate structured outputs with a runtime schema, then apply semantic, factual and authorization checks. Repair or retry malformed output within a bound. Generated code still needs ordinary engineering verification; a schema cannot establish correctness.

## Adversarial evaluation

Exercise malicious instructions in documents, code comments, web pages and tool output. Attempt cross-tenant retrieval, secret exfiltration, destination substitution, privilege escalation and a forged approval. Verify the executor denies unauthorized actions even if the model requests them.

Also test allowed tool failure, duplicate execution, rate limiting, stale state, cancellation, partial success, unknown outcomes and budget exhaustion. Evaluate whether the system stops safely and gives an actionable status. Prompt-only defenses must not be presented as a guarantee.

## Privacy, monitoring and degraded behavior

Map sensitive prompts, retrieval contents, traces, eval fixtures and tool results. Choose approved provider retention/training/residency settings and processors. Redact/minimize where appropriate and define deletion/access controls; never put production secrets into an evaluation dataset or model trace.

Monitor quality/eval drift, unsupported claims, user corrections, retrieval and tool errors, fallback frequency, latency, tokens and cost per successful task. Trace authorized tool activity without logging sensitive payloads. A lower-cost model, reduced context, deterministic path, human review or safe refusal can be a fallback; degraded modes must preserve permissions and safety.

## Foundations

[NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework), [AI-focused SSDF](https://csrc.nist.gov/pubs/sp/800/218/a/final), [OWASP GenAI](https://genai.owasp.org/). Adapted from master §23 and scenario H in §37. Verify provider-specific APIs and policy settings at execution time.
