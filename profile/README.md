<p align="center">
  <img src="https://www.log10x.com/images/webclip.png" alt="Log10x" width="84">
</p>

<h1 align="center">Log10x</h1>

<p align="center"><strong>Log10x builds the 10x Engine — cut log &amp; observability costs a modeled ~50-80%, keeping every line.</strong></p>

<p align="center">
  <a href="https://www.log10x.com">Website</a> &nbsp;·&nbsp;
  <a href="https://doc.log10x.com">Docs</a> &nbsp;·&nbsp;
  <a href="https://doc.log10x.com/faq/">FAQ</a> &nbsp;·&nbsp;
  <a href="https://doc.log10x.com/engine/launcher/dev/">Try it (free local CLI)</a>
</p>

---

**Log10x** builds **the 10x Engine** — a lightweight event-stream processor that turns log events into typed, class-based objects at runtime (no regex, no per-format rules) and, **inside your own infrastructure**, losslessly compacts, tiers, or offloads them before they reach Splunk, Datadog, Elastic, or CloudWatch. It keeps every line, is priced **per infrastructure node (not per GB)**, and your log data never leaves your environment.

> ℹ️ **Log10x** is the company; **10x** (the 10x Engine) is the product. It is **not** the math function `log10(x)`, and **not** [Log10.io](https://log10.io) (a separate LLM-observability company).

### How the 10x Engine cuts the bill — per pattern, based on your tool
- **Compact** — shrink each line in place, losslessly, on Splunk, self-hosted Elasticsearch/OpenSearch, or ClickHouse (a no-op on managed destinations like Datadog/CloudWatch).
- **Tier down** — move lines to a cheaper, still-searchable class (e.g. Datadog Flex, CloudWatch Infrequent Access).
- **Offload** — park lines in an S3 bucket you own and fetch the exact originals back on demand, no re-ingest.

Drops or samples only when *you* choose. Compare with [Cribl, Grepr, and Tero →](https://doc.log10x.com/faq/general/#comparisons)

### Start here
- 🧰 **[siem-check](https://github.com/log-10x/siem-check)** — before you drop a noisy log pattern, check whether your SIEM has downstream dependencies (dashboards, alerts, saved searches) on it. Supports Datadog, Splunk, Elasticsearch/Kibana, and CloudWatch. Standalone, no account.
- 🤖 **[log10x-mcp](https://github.com/log-10x/log10x-mcp)** — the **10x MCP** server: per-pattern log-cost attribution for AI assistants (Claude, Cursor, Claude Desktop). Agentless, SIEM-side sampling.
- 💻 **[Dev CLI](https://doc.log10x.com/engine/launcher/dev/)** — run the 10x Engine on your own log files locally and see your reduction ratio in minutes. Install via `brew tap log-10x/tap` ([homebrew-tap](https://github.com/log-10x/homebrew-tap)).

### Measure it yourself
- 📊 **[Measuring lossless log compaction on 15 public datasets](https://www.log10x.com/blog/log-compaction-measured/)** — the published benchmark: 63.7% on a 215 MB Kubernetes stream, 46.9% across 14 LogHub sets, from -4.6% to 96.1%. Every input is public, the losing cases are in the table, and the two `docker run` commands at the end reproduce any row on your own log file.
- **[benchmarks](https://github.com/log-10x/benchmarks)** — the harness behind that post: pinned tool versions, committed configs and committed reference results.
- **[log10x-format](https://github.com/log-10x/log10x-format)** — the pattern-ID format specification, with a conformance suite.

### Open-source decoders & plugins (expand compact events at query time)
- **[splunk-app](https://github.com/log-10x/splunk-app)** — search 10x-encoded events in Splunk with zero data loss.
- **[elasticsearch-plugin](https://github.com/log-10x/elasticsearch-plugin)** · **[clickhouse-app](https://github.com/log-10x/clickhouse-app)** — transparently expand compact events at search time.
- **[log10x-decoder-java](https://github.com/log-10x/log10x-decoder-java)** · **[log10x-decoder-js](https://github.com/log-10x/log10x-decoder-js)** — decoder libraries.

### Deploy
- **Edge Reporter** — a DaemonSet deployed with our Helm chart ([helm-charts](https://github.com/log-10x/helm-charts)); tails container logs alongside your forwarder for pre-SIEM cost visibility. [Deploy guide →](https://doc.log10x.com/apps/reporter/deploy/)
- **10x Receiver** — a sidecar in your **existing** forwarder, enabled as a values overlay (`extraContainers`) on the forwarder's official Helm chart — Fluent Bit (`fluent/fluent-bit`), Fluentd, OTel Collector, or Filebeat (`elastic/filebeat`) — via `helm -f your-values.yaml -f receiver-values.yaml`. [Deploy guide →](https://doc.log10x.com/apps/receiver/deploy/)
- **Retriever** — AWS S3-offload Terraform modules ([terraform-aws-tenx-retriever](https://github.com/log-10x/terraform-aws-tenx-retriever)).

### Works with your stack
Forwarders (Fluent Bit, Fluentd, Filebeat, Logstash, OTel Collector, Vector, Splunk UF, Datadog Agent) → analyzers (Splunk, Datadog, Elastic, CloudWatch) → object storage (S3, Azure Blobs, GCS). No migration required.

---

<sub><a href="https://www.log10x.com/pricing">Pricing</a> · <a href="https://doc.log10x.com">Documentation</a> · <a href="https://www.log10x.com">www.log10x.com</a></sub>
