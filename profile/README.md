<p align="center">
  <img src="https://www.log10x.com/images/webclip.png" alt="Log10x" width="84">
</p>

<h1 align="center">Log10x</h1>

<p align="center"><strong>Log10x builds the 10x Engine: control log &amp; observability costs, pattern by pattern.</strong></p>

<p align="center">
  <a href="https://www.log10x.com">Website</a> &nbsp;·&nbsp;
  <a href="https://doc.log10x.com">Docs</a> &nbsp;·&nbsp;
  <a href="https://doc.log10x.com/faq/">FAQ</a> &nbsp;·&nbsp;
  <a href="https://doc.log10x.com/engine/launcher/dev/">Try it (free local CLI)</a>
</p>

---

**Log10x** builds **the 10x Engine**, a lightweight event-stream processor that runs **inside the customer's own infrastructure**. It names each log line from a symbol library compiled ahead of time from source, binaries and container images (no regex, no per-format rules, nothing learned at run time), and per pattern it chooses the lines to tier down, offload, or (on Splunk and self-managed Elasticsearch) losslessly compact before they reach Splunk, Datadog, Elastic, or CloudWatch. Compact, tier down and offload keep every line. Priced **per infrastructure node, not per GB**; log data never leaves the customer's environment.

> ℹ️ **Log10x** is the company; **10x** (the 10x Engine) is the product. It is **not** the math function `log10(x)`, and **not** [Log10.io](https://log10.io) (a separate LLM-observability company).

### Three levers, by destination
- **Compact**: shrink each line in place, losslessly, on Splunk and self-managed Elasticsearch/OpenSearch; 10x encodes at the edge and expands at search time. A no-op on managed destinations like Datadog and CloudWatch.
- **Tier down**: choose the lines a platform's own cheaper, still-searchable tier stores (Datadog Flex, CloudWatch Infrequent Access, Azure Basic, Elastic frozen). The rule keys on the pattern, the same on every pod from its first line.
- **Offload**: ship lines to an S3 bucket the customer owns, indexed as they land, and stream the originals back into the SIEM on demand, found by key without a scan.

Sample and drop, the Receiver's Filter modes, run only when the operator chooses them. Compare with [Cribl, Grepr, and Tero →](https://doc.log10x.com/faq/general/#comparisons)

### Start here
- 🧰 **[siem-check](https://github.com/log-10x/siem-check)**: checks whether a noisy log pattern has downstream dependencies in the SIEM (dashboards, alerts, saved searches) before it is dropped. Supports Datadog, Splunk, Elasticsearch/Kibana, and CloudWatch. Standalone, no account.
- 🤖 **[log10x-mcp](https://github.com/log-10x/log10x-mcp)**: the **10x MCP** server, per-pattern log-cost attribution for AI assistants (Claude, Cursor, Claude Desktop); agentless, with sampling on the SIEM side.
- 💻 **[Dev CLI](https://doc.log10x.com/engine/launcher/dev/)**: runs the 10x Engine locally on a log file and reports its reduction ratio in minutes. Install via `brew tap log-10x/tap` ([homebrew-tap](https://github.com/log-10x/homebrew-tap)).

### Measure it yourself
- 📊 **[Splunk license meter](https://github.com/log-10x/benchmarks/tree/main/splunk-license)**: Splunk's license meter counted 63.91% fewer bytes on one OpenTelemetry demo capture through a Universal Forwarder, encoded events and templates included, and every event expands back byte for byte.
- 📊 **[Log compaction that stays searchable, measured on 15 public datasets](https://www.log10x.com/blog/log-compaction-measured/)**: file ratios, 64% on a 215 MB stream from a 36-container OpenTelemetry demo cluster, metadata and templates included; across 14 LogHub datasets, 4.7% to 58.4%, byte-weighted 44.7%. Every input is public, and the two `docker run` commands at the end reproduce any row and measure any other log file the same way.
- **[benchmarks](https://github.com/log-10x/benchmarks)**: the harnesses behind these figures, the Datadog Flex and CloudWatch Infrequent Access accounting runs, and the pattern-identity comparison with Drain3; pinned tool versions, committed configs and committed reference results.
- **[log10x-format](https://github.com/log-10x/log10x-format)**: the pattern-ID format specification, with a conformance suite.

### Open-source decoders & plugins (expand compact events at query time)
- **[splunk-app](https://github.com/log-10x/splunk-app)**: the 10x Splunk app ([Splunkbase 9866](https://splunkbase.splunk.com/app/9866)) expands compact events at search time.
- **[elasticsearch-plugin](https://github.com/log-10x/elasticsearch-plugin)**: expands compact events at search time in self-managed Elasticsearch 8.17 and OpenSearch 2.19.
- **[log10x-decoder-java](https://github.com/log-10x/log10x-decoder-java)** · **[log10x-decoder-js](https://github.com/log-10x/log10x-decoder-js)**: decoder libraries.

### Deploy
- **Reporter**: a DaemonSet deployed with our Helm chart ([helm-charts](https://github.com/log-10x/helm-charts)); tails container logs alongside the existing forwarder for pre-SIEM cost visibility. [Deploy guide →](https://doc.log10x.com/apps/reporter/deploy/)
- **10x Receiver**: a sidecar in the **existing** forwarder, enabled as a values overlay (`extraContainers`) on the forwarder's official Helm chart for Fluent Bit (`fluent/fluent-bit`), Fluentd, OTel Collector, or Filebeat (`elastic/filebeat`), via `helm -f your-values.yaml -f receiver-values.yaml`. [Deploy guide →](https://doc.log10x.com/apps/receiver/deploy/)
- **Retriever**: AWS S3-offload Terraform modules ([terraform-aws-tenx-retriever](https://github.com/log-10x/terraform-aws-tenx-retriever)).

### Integrations
Forwarders (Fluent Bit, Fluentd, Filebeat, Logstash, OTel Collector, Vector, Splunk UF, Datadog Agent) → analyzers (Splunk, Datadog, Elastic, CloudWatch) → object storage (S3 and S3-compatible stores).

---

<sub><a href="https://www.log10x.com/pricing">Pricing</a> · <a href="https://doc.log10x.com">Documentation</a> · <a href="https://www.log10x.com">www.log10x.com</a></sub>
