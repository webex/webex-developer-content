---
type: Article
title: 'From Waveform to Insight: A Compiler for Customer Intent'
canonical_url: https://developer.webex.com/blog/from-waveform-to-insight-topic-analytics
content_type: blog
date: '2026-05-19'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/from-waveform-to-insight-topic-analytics)

<p>
  Every contact center sits on the same paradox: the most valuable signal in the
  business — <em>why customers are actually calling</em> — flows past in a medium
  (speech) that almost no downstream system can consume. Analytics dashboards
  speak in joinable rows and columns; conversations arrive as waveforms. The gap
  between those two representations is where containment strategies die, where
  staffing plans go stale, and where emerging issues incubate for weeks before
  anyone notices.
</p>

<p>
  <strong>Topic Analytics</strong> is how we close that gap. And the useful way to
  think about it is not as a dashboard or a report, but as a <em>semantic compiler</em>:
  a multi-stage pipeline that lowers acoustic signal into a typed, clustered, labeled
  ontology of customer intent — in near real time, on every interaction, at contact-center
  scale.
</p>

<blockquote>
  A compiler takes a language humans write fluently but machines cannot reliably
  execute — loose, ambiguous, full of context only a reader can resolve — and
  lowers it, stage by stage, into symbolic instructions a machine can act on.
  Topic Analytics is the same idea, applied to the language humans speak most
  fluently of all: conversation. Free-form, discursive, full of digressions and
  repairs — and, until now, completely opaque to any database downstream of it.
  The pipeline lowers it into symbols a BI system can join on.
</blockquote>

<br />

<h3>The problem, stated precisely</h3>

<p>
  Contact center supervisors are under pressure to improve containment (deflect more
  to self-service), lift agent productivity, and protect CSAT. Each of those
  levers depends on a single upstream primitive: <strong>a reliable, current
  distribution of contact reasons</strong>. Without it, you cannot:
</p>

<ul>
  <li>Pick the right automation candidates — the topics with the highest volume and lowest variance in intent.</li>
  <li>Plan staffing and training against <em>real</em> demand rather than last quarter's call codes.</li>
  <li>Detect emerging issues while they are still faint, before a mis-priced SKU or a broken deployment becomes a CSAT cliff.</li>
</ul>

<p>
  The incumbent answer — agent-selected disposition codes plus sampled manual
  QA — is slow, biased, and low-resolution. It answers "what did an agent
  remember to click after a call?" not "what is the population of customer
  intents right now?"
</p>

<hr />

<br />

<h3>Architecture: a seven-stage pipeline</h3>

<p>
  Topic Analytics is engineered as a purpose-built pipeline for contact-center
  interactions, rather than a general-purpose NLP toolkit bolted onto the side
  of the platform. Each stage is independently scalable and independently
  evaluable, and each stage's output is the next stage's typed input.
</p>

<p><img alt="Seven-stage Topic Analytics pipeline" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt55656a1e0f925f40/6a172d941949f7450be7add0/topic-analytics-pipeline-bright.svg" /></p>

<p><em><b>Figure 1.</b> The pipeline. Stages 1–7 run per-interaction in near real time; stage 6 feeds a slower, continuous retraining loop back into stage 4.</em></p>

<h4>Stage 1: Speech-to-Text transcription</h4>

<p>Streaming ASR optimized for the phonetic and prosodic characteristics of contact-center audio — narrow-band telephony codecs, accented speakers, background noise, hold music. Because the caller leg and the agent leg are captured and processed as <em>separate</em> audio streams, transcripts are produced with speaker labels directly — no ML diarization model required to untangle who said what. The two streams are stitched back together with clean provenance on every utterance, which matters downstream: distinguishing the customer's words from the agent's is essential when we go looking for the <em>customer's</em> reason for contact.</p>

<h4>Stage 2: Redaction</h4>

<p>Before any transcript touches the LLM, it passes through a PII-aware redactor. Named entities, account numbers, payment credentials, dates of birth, and health data are replaced with typed placeholders (<code>&lt;CARD_NUMBER&gt;</code>, <code>&lt;DOB&gt;</code>). This is not just a compliance boundary — it is an <em>information-theoretic</em> boundary. Redacting tokens that would otherwise dominate attention weights (long digit spans, proper nouns) forces the extraction model to condition on the actual intent phrases, which improves topic coherence downstream.</p>

<h4>Stage 3: LLM-powered contact-reason extraction</h4>

<p>A purpose-prompted LLM reads the redacted transcript and emits a compact, canonicalized phrase that captures the customer's <em>reason for contact</em> — not a summary, not a sentiment, not an agent action. A flight-status call becomes <code>"check flight delay status"</code>; a billing call becomes <code>"dispute duplicate charge"</code>. Producing a normalized reason phrase — rather than trying to cluster the full transcript — is what makes the rest of the pipeline tractable.</p>

<h4>Stage 4: Dynamic clustering</h4>

<p>Reason phrases are embedded into a dense vector space. Clusters are discovered <em>dynamically</em> — the number of topics is not fixed in advance — using an <strong>incremental clustering algorithm</strong> that assigns each new point online as it arrives, spawns a new cluster when no existing region is a sufficiently good neighbor, and lets clusters evolve as more data accumulates. Because the algorithm is incremental rather than batch, it is what makes the "near" in near real time possible: we are not re-running a batch clustering algorithm over a historical window on every tick, we are updating the topic space as each interaction lands. (An earlier generation of Topic Analytics was built on a batch clustering algorithm; the NRT system is not.) This is the stage that lets a new product launch or a novel defect manifest as a new topic within hours, not quarters.</p>

<h4>Stage 5: Automatic topic labeling</h4>

<p>Each cluster is named by a second LLM pass that reads a sample of its member phrases and produces a 2–3 word human-readable label (<code>Flight status</code>, <code>Refund request</code>, <code>Baggage help</code>). Labels are constrained to be noun-phrase-shaped and terminology-aware — the model has context about the customer's industry so it favors <em>domain</em> language over <em>generic</em> language.</p>

<h4>Stage 6: User-centric topic customization</h4>

<p>AI-generated topics are a starting point, not an endpoint. Admins can seed pre-defined topics at configuration time (typed in, or uploaded as CSV/XLSX), rename AI-generated labels, and merge clusters that the model split too finely. Those human edits are first-class signals: they flow back into the clustering stage as soft constraints on the next run. This is the difference between "the AI is wrong, retrain it" and "the AI learned what <em>your</em> business calls that thing."</p>

<h4>Stage 7: Continuous insights</h4>

<p>The final stage is the one that makes the rest useful: emitting topic assignments as typed fields on every interaction, available in the Analyzer dashboard and over the API as custom report columns (<code>Topic Name</code>, <code>Contact Driver</code>). This is where the pipeline re-enters the BI world. You can now <code>GROUP BY topic</code> and ask the real questions: which topics have the worst CSAT? the longest AHT? the steepest week-over-week growth?</p>

<blockquote><p><strong>The loop is the product.</strong> A one-shot topic model decays the moment the business changes. Topic Analytics is explicitly designed as a closed loop: human curation in stage 6 becomes training signal for stage 4, which changes the labels stage 5 generates, which surfaces new topics to curate in stage 6. The dashboards are the <em>readout</em> of a system that is always learning the shape of <em>your</em> demand.</p></blockquote>

<hr />

<br />

<h3>A seismograph, not a thermometer</h3>

<p>
  The second metaphor that is useful here: Topic Analytics is a <em>seismograph</em>,
  not a thermometer. A thermometer reports a scalar — call volume is up, CSAT is
  down — and by the time a thermometer reading becomes alarming, the event has
  already happened. A seismograph picks up weak signals spatially distributed
  across a surface and lets you see the tremor <em>where</em> it originated,
  long before it becomes an earthquake.
</p>

<p>
  Because every interaction is labeled, not just a sample, the system can detect
  cluster-level anomalies: a topic that did not exist last week, a topic whose
  handle time doubled overnight, a topic whose CSAT collapsed on a specific
  queue. These are the faint tremors — the single-digit percentage shifts in the
  tail — that predict the headline incident.
</p>

<p><img alt="Topic volume as a seismograph over time" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2ff2df7e605a7631/6a172d95961e6901a1c4d21e/topic-analytics-seismograph-bright.svg" /></p>

<p><em><b>Figure 2.</b> Known topics track their baselines; a novel cluster — call it &quot;boarding-pass app error&quot; — appears at week 3 and spikes at week 4. Topic Analytics names and surfaces it <em>while it is still small</em>, not after it tops the volume chart.</em></p>

<hr />

<br />

<h3>Why the embedding space shape matters</h3>

<p>
  The design choice that carries the most weight is actually stage 4: <em>incremental,
  online</em> clustering on extracted reason phrases, rather than classification
  into a fixed taxonomy. The implication is worth stating plainly.
</p>

<p>
  A fixed-taxonomy classifier is a decision about the world frozen at training time.
  When a new SKU launches, when a regulatory change creates a new category of call,
  when two previously distinct topics merge because the business process unified —
  a classifier cannot tell you, because it does not have a label for the thing it
  is seeing. It will quietly bucket the new calls into the nearest existing class,
  and the dashboard will continue to look normal.
</p>

<p>
  Incremental online clustering is the opposite. Each new reason phrase is
  compared against the current cluster structure as it arrives; points that are
  not a sufficiently good fit for any existing region are <em>allowed to remain
  unassigned</em> until enough of them accumulate to form their own. When that
  region crosses the threshold, a new cluster is born, stage 5 names it, and it
  starts producing dashboard readings — without any offline retraining step.
  The system's ontology tracks the business's ontology, on its own.
</p>

<p><img alt="Embedding space before and after a new topic emerges" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt20d41cb5703af29d/6a172d96b339d5066276a319/topic-analytics-embedding-space-bright.svg" /></p>

<p><em><b>Figure 3.</b> The same embedding space, three weeks apart. A new high-density region crosses the cluster-birth threshold and gets named automatically. A fixed-taxonomy system would have silently buried these calls in &quot;Other.&quot;</em></p>

<hr />

<br />

<h3>What this looks like at the edge — the surface area</h3>

<p>
  Inside the product, the compiler's output shows up in three surfaces:
</p>

<br />

<h3>1. The Topic Analytics dashboard</h3>

<p>
  The primary UI — the one that ops leaders live in — is organized around the
  questions the pipeline was built to answer. Highest interaction volume. Longest
  average handle time. Highest and lowest CSAT. Top five topics by trend.
  Trending-topics table with per-topic sample-contact drill-down, filterable by
  queue and time window, refreshable on demand. This is the readout.
</p>

<p><img alt="Topic Analytics dashboard: volume cards, Top 5 topics trend chart, top topics by CSAT and average handle time, Trending topics table" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4d499a99a7d0e216/6a172d93961e6929efc4d21a/topic-analytics-dashboard.png" /></p>

<p><em><b>Figure 4.</b> The Topic Analytics dashboard. The entire compiler stack exists to make this view possible — every card and column is a <code>GROUP BY topic</code> away from the raw interaction stream.</em></p>

<br />

<h3>2. Topic drill-down</h3>

<p>
  For any single topic you can pivot into <em>that topic's world</em>: its
  volume curve over time, its channel mix (voice / chat / email / SMS), the
  full list of associated interactions, and — crucially — the actual
  transcripts. The compiler can be trusted, but you can always inspect what it
  compiled.
</p>

<p><img alt="Topic drill-down view for the Flight status topic: performance-over-time chart, interaction-by-channel breakdown, associated-interactions table" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcac0defeea81a07e/6a172d93c1e8a578f5f885f8/topic-analytics-drilldown.png" /></p>

<p><em><b>Figure 5.</b> Topic drill-down. Every aggregate statistic is traceable back to the individual conversations that produced it — the compiler&#x27;s output is always inspectable.</em></p>

<br />

<h3>3. Analyzer + API</h3>

<p>
  Two new custom fields — <code>Topic Name</code> and <code>Contact Driver</code> —
  are exposed as first-class columns inside the Analyzer reporting engine and
  over the public API. The same fields that power the native dashboards are
  available to your existing reports, your data warehouse, and your
  BI stack. The output of the pipeline is not a walled garden; it is a join key.
</p>

```sql
// Example: join your existing interaction warehouse to Topic Analytics output
SELECT
  t.topic_name,
  COUNT(*)                            AS interactions,
  AVG(i.handle_time_s)              AS avg_aht,
  AVG(i.auto_csat)                  AS avg_csat,
  COUNT(*) FILTER (WHERE i.contained) AS deflected
FROM   interactions i
JOIN   topic_analytics t USING (interaction_id)
WHERE  i.created_at >= '2026-04-01'
GROUP BY t.topic_name
ORDER BY interactions DESC;
```

<p>
  That query — a week of contact-center demand, sliced by intent, with automation
  and CSAT signal attached — is the one an ops leader could not write at all
  before, because the <code>topic_name</code> column did not exist. The entire
  pipeline is the machinery required to make one join key meaningful.
</p>

<hr />

<br />

<h3>The engineering problems this actually solves</h3>

<h4>Cold start</h4>

<p>
  A clustering system needs data before it can cluster. Most tenants do not want
  to run blind while the model learns what their calls are about. Pre-defined
  topics solve this: admins seed an initial topic list at configuration time
  (typed or uploaded as a CSV/XLSX), and those names are matched against
  interactions from day one. AI-generated topics accumulate alongside the
  pre-defined ones, and the pre-defined list provides anchors that stabilize
  the embedding space while the long tail is being discovered.
</p>

<h4>Label drift</h4>

<p>
  LLM-generated labels are a moving target — the same cluster can get named
  "Refund request" one day and "Request for refund" the next if you are not
  careful. The system pins labels to cluster identity, not to generation runs,
  so the same cluster keeps its name across re-runs unless an admin renames it
  (which then becomes the pinned label, overriding the AI).
</p>

<h4>Long-tail topics</h4>

<p>
  In a realistic contact center, the distribution is heavy-tailed: the top 20
  topics are 80% of volume, and there are thousands of rare intents in the
  tail. Incremental online clustering is well-suited to this — it will form a
  cluster for a rare intent once enough related points have arrived, and leave
  individual oddities unassigned until they find neighbors. The tail remains
  inspectable without drowning the dashboard.
</p>

<h4>Cross-language support</h4>

<p>
  The April–June 2026 release extends the pipeline to multi-language voice
  interactions and to digital channels (chat, email, SMS) — including AI-agent
  interactions, which close the loop between automation and the analytics
  that tell you whether the automation is actually working. The architecture
  accommodates this because every stage from redaction onward operates on
  text in a language-general way, with only stage 1 (ASR) and the extraction
  prompt in stage 3 needing to be language-aware.
</p>

<hr />

<br />

<h3>Where this goes next</h3>

<p>
  The roadmap telegraphs the ambition. Shipped in Q1 2026: near real-time
  discovery and pre-defined topic names. Shipping this quarter: multi-language
  voice, digital interactions, and AI Agent interactions. On the horizon:
  <strong>topic-to-AI-agent creation</strong> — the system identifies a
  high-volume topic with low variance in intent, and offers to generate an
  AI agent scoped to that topic. Topic themes for hierarchical organization.
  Topic insights for automated narrative over the trend data.
</p>

<p>
  That last one — topic-to-agent — is the closing of the biggest loop in the
  contact center. Today, Topic Analytics tells you which calls are the best
  candidates for automation. Tomorrow, it builds the automation. The compiler
  stops describing the program and starts writing it.
</p>

<blockquote>
  Every contact center has always had its reasons-for-contact. They were just
  encoded in a medium — audio — that no dashboard could read. Topic Analytics
  is the translation layer: it lowers conversation into a joinable fact, and
  it does so continuously, on every interaction, in the business's own
  language. The dashboards are downstream. The pipeline is the point.
</blockquote>

<hr />

<br />

<h3>About the authors</h3>

<p><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4bd358908496de5c/6a172d97d7c022e9fede680d/topic-analytics-francis-kurupacheril-headshot.jpeg?width=220" alt="Francis Kurupacheril headshot" width="180" /></p>

<p><strong>Francis Kurupacheril</strong> is a seasoned technology executive and product strategist with over 27 years of experience delivering transformative AI and SaaS innovations across enterprise and consumer platforms, and serves as Director of Product Management at Cisco, where he leads the company's GenAI and Language AI strategy for the Webex portfolio.</p>

<p>At Cisco, Francis has architected and operationalized a multi-layered AI platform powering over 23 million meeting summaries and over a trillion LLM tokens processed. An expert in LLM productization, responsible AI, and agent-based architectures, Francis has scaled AI systems with multi-model support (OpenAI, Claude, Cisco-native models), achieving over 5x cost efficiency in key use cases. He has overseen delivery across AI-driven collaboration features, semantic graph search, topic analytics, and multi-modal assistants, impacting daily productivity for millions of enterprise users. His initiatives around agentic collaboration platforms are positioning Cisco as a trusted AI partner for government and regulated industries.</p>

<p><img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc4a9c5e2e9cd5d78/6a172d98b339d561c476a31d/topic-analytics-jason-vaccaro-headshot.png?width=220" alt="Jason Vaccaro headshot" width="180" /></p>

<p><strong>Jason Vaccaro</strong> is a Software Engineering Technical Leader for CollabAI. He has led the Topic Analytics project for the last two years. He has been at Cisco for four years and JP Morgan Chase &amp; Co for four years before that. Jason graduated from Columbia University with a bachelor's in computer science and a concentration in mathematics.</p>

<p>At Cisco, Jason leads application development on AI-centered projects. He is particularly passionate about building distributed systems that scale, cutting infrastructure costs, and improving observability. Jason mentors junior engineers to promote their professional development and boost team velocity. He facilitates group discussions and brainstorm sessions to foster collaboration and improve design decisions.</p>
