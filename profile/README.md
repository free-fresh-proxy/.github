<p align="center">
  <img src="https://github.com/user-attachments/assets/9afb9345-7cc5-4743-983b-640dfcf0c0d8" alt="Free Fresh Proxy logo" width="96" />
</p>

<h1 align="center">Free Fresh Proxy</h1>

<p align="center">
  <em>A free proxy service that updates its proxy list every hour. <br>All proxies run on our own infrastructure — fast, stable, no third-party intermediaries.</em>
</p>

<p align="center">
  <a href="https://share.google/qnHnGGeHek4han5el"><img src="https://github.com/user-attachments/assets/2fac9c18-7695-4626-b7f2-74b6de32da64" alt="Hourly refresh" /></a>
</p>

---

<table>
<tr>
<td width="55%" valign="top">

### What Free Fresh Proxy is

Free Fresh Proxy is a free proxy service that refreshes its proxy list every hour. All proxies run on our own infrastructure, so you get fast and stable endpoints without third-party intermediaries.

If you've ever pulled a proxy list from a public aggregator and found half the entries dead, you know the problem this solves. Every hour, the list is rebuilt from live nodes on our servers. What you pull is what's actually working.

The service is built for developers — testing how your app behaves from a different network, scraping public data, automating requests, or checking geo-specific behavior. No accounts, no hidden paywalls, no middlemen reselling someone else's capacity.

</td>
<td width="45%" valign="top">
<br>
<br>
<img src="https://github.com/user-attachments/assets/e5d1604d-4a59-4a1e-94f5-ee871d3dfae7" alt="Free Fresh Proxy dashboard showing the current proxy list" width="100%" />


</td>
</tr>
</table>

---

### How the refresh works

The list is rebuilt on a fixed hourly schedule. Between refreshes, the current list stays stable — you can cache it, diff it, or pull it on your own schedule without surprises.

**Every hour, three things happen:**

1. **Health checks run** against every node on our infrastructure. Nodes that fail are removed from the pool.
2. **New nodes come online** as capacity is added or rotated. They appear in the next refresh.
3. **The published list is rebuilt** from the surviving nodes, with metadata (protocol, region, latency) attached to each entry.

Between refreshes, the list is static. That means you can diff two consecutive pulls and see exactly what changed — useful if you're tracking uptime or building a rotation strategy.

---

<table>
<tr>
<td width="45%" valign="top">
<br>
<br>
<br>
<br>
<br>
<img src="https://github.com/user-attachments/assets/dde567f4-b566-4748-a94d-e401dc931225" alt="Free Fresh Proxy node health and latency view" width="100%" />

</td>
<td width="55%" valign="top">

### What you actually get

**A live list, not an archive.** The published list contains only nodes that passed health checks in the most recent cycle. Dead entries don't linger.

**Metadata per entry.** Protocol (HTTP, HTTPS, SOCKS5), region, and measured latency are attached to each node — enough to pick intelligently without testing every one yourself.

**Our own infrastructure.** Nodes run on servers we operate. When something breaks, we fix it. When capacity changes, it shows up in the next refresh — not whenever a reseller decides to update their page.

**No accounts, no API keys.** Pull the list, use it. If fair-use rate limits apply, they're documented — not hidden behind a signup form.

**Developer-oriented format.** The list is published in plain text and JSON, easy to parse, easy to cache, easy to diff.

</td>
</tr>
</table>

---

### Who this is for

**Developers testing network behavior.** Check how your application responds when requests originate from a different region or IP range.

**People scraping public data.** Distribute requests across endpoints to avoid hammering a single source, within the limits of the target site's terms.

**Automation and CI.** Run integration tests that need outbound requests from varied origins.

**Anyone learning how proxies work.** Pull a list, watch it change hour by hour, see which nodes survive health checks. It's a useful way to understand how proxy rotation actually behaves.

---

### Fair use and limits

The service is free, but not unlimited. To keep it available for everyone, the following apply:

- **Rate limits on the list endpoint.** Pulling the list more than a few times per hour won't return different data — the list only changes on the hour.
- **Per-IP concurrency limits.** A single client hammering many nodes simultaneously will be throttled.
- **No abuse.** Using the proxies for spam, credential stuffing, scraping sites that forbid it, or attacking third parties will get your access blocked — and may be reported.

These limits exist so the service stays up. They're documented, not hidden.

---

### Common questions

**Is it really free?**
Yes. No accounts, no payment, no trial period. The infrastructure is ours, and the service is offered as-is.

**How often does the list change?**
Every hour. Nodes that fail health checks are removed; new nodes appear in the next refresh.

**Can I use it in production?**
For testing and low-volume automation, yes. For high-volume production traffic, you should run your own proxies — this service is shared.

**Do you log traffic?**
We log connection metadata (timestamps, node, request counts) for health checks and abuse prevention. We don't inspect payloads. Details are in the privacy section below.

**What protocols are supported?**
HTTP, HTTPS, and SOCKS5. Each entry in the JSON list indicates its protocol.

**What happens if a node goes down mid-use?**
Your request fails. The next pull of the list won't include that node. Build retry logic into your client — it's normal for any proxy pool.

**Can I get a dedicated proxy?**
Not through this service. It's a shared pool by design.

---

### When something doesn't work

| Symptom | Likely cause | First step |
| :--- | :--- | :--- |
| List endpoint returns empty | Service maintenance or outage | Check the status page, retry after the hour |
| Proxies connect but requests fail | Target site blocks proxy IPs | Try a different node, check target site's terms |
| High latency across all nodes | Network conditions on your side | Test from a different network to isolate |
| Rate-limited on the list endpoint | Pulling too frequently | Pull once per hour, cache the result |
| A node stops working mid-session | Node failed health check | Pull the fresh list, retry with a new node |
| SOCKS5 nodes fail but HTTP works | Client misconfiguration | Verify your client supports SOCKS5 correctly |

---

### Privacy and logging

We log connection metadata — timestamps, which node was used, request counts per IP — for two purposes: health checks and abuse prevention. We do not inspect request payloads, and we do not sell or share logs with third parties.

If you're handling sensitive traffic, don't route it through a shared proxy pool. Use a proxy you control.

---

### Contributing

Bug reports, documentation fixes, and client examples are welcome. If you've built a useful client wrapper or integration, open a pull request — it helps other developers get started faster. When reporting an issue, include the endpoint you pulled, the timestamp, and what you expected versus what you got.

---

### The fine print

Free Fresh Proxy is maintained by our team and runs on our own infrastructure. The service is provided as-is, without warranty. You are responsible for how you use the proxies and for complying with the terms of any site you access through them. Abuse — spam, credential stuffing, attacks on third parties — will result in blocked access and may be reported to the relevant parties.

---

<p align="center">
  <sub>free proxy service · free proxy list · hourly proxy refresh · fresh proxies every hour · own proxy infrastructure · http proxy · https proxy · socks5 proxy · proxy list for developers · proxy api · free proxies for scraping · proxy rotation · proxy pool · developer proxy service · free proxy json · proxy list plain text · no-account proxy · self-hosted proxy network · free proxy endpoints · proxy health checks</sub>
</p>
