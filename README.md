# vps with dedicated cores: What "Dedicated" Actually Gets You, Which GreenCloud Plans Qualify, and What $10/mo Buys

When people search for a VPS with dedicated cores, they're usually dealing with the same problem: CPU performance that swings wildly depending on what neighbors on the same physical host are doing. Compile jobs that take 2 minutes one day and 9 the next, database queries with random latency spikes, steal time showing up in `top` out of nowhere. A VPS with dedicated cores fixes that by pinning physical CPU cores to your instance so no other tenant can touch them.

The catch is that "dedicated" gets thrown around loosely in this market. Some hosts mean genuinely reserved physical cores. Others just mean "you have 4 vCPUs" that are shared like everyone else's. This guide sorts out the difference, then looks at one of the more affordable ways to actually get reserved cores: GreenCloud's EPYC VDS line, which starts at $10/month for 1 dedicated EPYC core with 8GB RAM and 80GB NVMe storage.

> **Quick take:** If your workload needs predictable CPU — production databases, game servers, compile farms, latency-sensitive apps — the **EPYCVDS-1** ($10/mo, 1 dedicated EPYC Milan core, 8GB RAM, 80GB NVMe, 10Gbps port) is the entry point. Lighter workloads that don't need CPU guarantees can drop to GreenCloud's shared-core Ryzen or Budget KVM lines at $6/mo. **👉 [Check GreenCloud's dedicated-core VDS plans and current locations](https://greencloudvps.com/billing/aff.php?aff=6679)**

## Dedicated cores vs. regular vCPUs: what's the actual difference?

A regular VPS gives you virtual CPU cores carved out of a physical processor that's shared among many virtual machines. The host oversubscribes — that's how $5 VPS plans exist — and when a neighbor hits its CPU hard, your available cycles dip. You still "have" 2 or 4 cores on paper. You just don't always get them.

A VDS (virtual dedicated server) with dedicated cores works differently. Physical cores are reserved exclusively for your instance. Contabo describes the distinction clearly on its own site: a VDS has "its own reserved CPU cores and RAM, carved out of a physical host by a hypervisor — no other tenant can touch your allocated resources," while a dedicated server is the entire physical machine. The VDS sits between shared VPS and bare metal: guaranteed cores, but you're still one of several VMs on the host.

A few related terms you'll see, roughly meaning the same thing:

- **Core pinning** — your VM's vCPUs are pinned to specific physical cores. Some providers (like RackWorks, whose pinned-core plans start at $25/mo) go further and pin all cores to a single NUMA socket so CPU and RAM access stay local and avoid cross-socket latency.
- **No oversubscription / no steal time** — providers like VPSLab advertise Ryzen 9 9950X cores "pinned via KVM: no oversubscription, no steal time." Steal time is the metric to watch: if it sits near 0%, nobody is taking your cycles.

None of this matters for every workload. A blog, a VPN endpoint, or a small WordPress site will never notice the difference. The keyword search makes sense when CPU consistency is the product: trading platforms, databases with SLA-bound queries, Minecraft servers with 50+ players, CI runners, game servers where tick rate dips are visible.

## GreenCloud's plans: the dedicated-core line and the shared-core lines

GreenCloud (greencloudvps.com, run by 365 Group LLC, in business since 2013) splits its KVM lineup the same way. Only one line actually gives you dedicated cores — the EPYC NVMe KVM VDS. The Ryzen and Budget KVM lines are conventional shared-core VPS. Here's the full current lineup, all Linux-only, all on 10Gbps ports:

**EPYC NVMe KVM VDS — dedicated cores (the line this keyword is about):**

| Plan | Dedicated CPU | RAM | NVMe Storage | Bandwidth (US/EU) | Price |
| --- | --- | --- | --- | --- | --- |
| EPYCVDS-1 | 1× EPYC Milan core | 8GB | 80GB | 4TB | $10/mo |
| EPYCVDS-2 | 2× dedicated cores | 16GB | 160GB | 8TB | $20/mo |
| EPYCVDS-3 | 3× dedicated cores | 24GB | 240GB | 12TB | $30/mo |
| EPYCVDS-4 | 4× dedicated cores | 32GB | 320GB | 16TB | $40/mo |
| EPYCVDS-5 | 8× dedicated cores | 64GB | 640GB | 16TB | $80/mo |

[👉 Order a dedicated-core EPYC VDS plan](https://greencloudvps.com/billing/aff.php?aff=6679) · APAC locations (Singapore, Tokyo, Hong Kong, Vietnam) come with half the bandwidth at the same price — more on that below.

**Ryzen KVM VPS — shared cores, high clock speed:**

| Plan | CPU | RAM | NVMe | Bandwidth (US/EU) | Price |
| --- | --- | --- | --- | --- | --- |
| RyzenKVM-1 | 1 core @ 3.5+ GHz | 1GB | 15GB | 1.5TB | $6/mo |
| RyzenKVM-2 | 1 core @ 3.5+ GHz | 2GB | 30GB | 2TB | $10/mo |
| RyzenKVM-3 | 2 cores @ 3.5+ GHz | 4GB | 50GB | 4TB | $20/mo |
| RyzenKVM-4 | 4 cores @ 3.5+ GHz | 8GB | 80GB | 8TB | $40/mo |
| RyzenKVM-5 | 8 cores @ 3.5+ GHz | 16GB | 150GB | 12TB | $80/mo |

**Budget KVM VPS — shared cores, cheapest entry:**

| Plan | CPU | RAM | SSD | Bandwidth (US/EU) | Price |
| --- | --- | --- | --- | --- | --- |
| SSDKVM-1 | 1 core | 1GB | 15GB | 1.5TB | $6/mo |
| SSDKVM-2 | 1 core | 2GB | 15GB | 2TB | $10/mo |
| SSDKVM-3 | 2 cores | 4GB | 30GB | 4TB | $20/mo |
| SSDKVM-4 | 4 cores | 8GB | 60GB | 8TB | $40/mo |
| SSDKVM-5 | 8 cores | 16GB | 120GB | 12TB | $80/mo |

GreenCloud also runs periodic flash sales and a "Premium KVM Sale" line (small EPYC-based plans like 2GB/25GB NVMe and 8GB/60GB NVMe in US and Canadian datacenters, managed through the VirtFusion panel), plus Windows VPS, storage VPS, and dedicated servers. Promo plans rotate and sell out by location — at the time of checking, Dallas, Toronto, San Jose and Chicago had stock while New York, Los Angeles, Ashburn and Amsterdam were sold out — so treat any promo table as a snapshot rather than a promise.

## The price math: what a dedicated core actually costs you here

This is the part most comparison posts skip, and it's where GreenCloud's lineup gets interesting. Compare the $10 plans across the three lines:

- **$10/mo, Budget KVM (SSDKVM-2):** 1 shared core, 2GB RAM, 15GB SSD
- **$10/mo, Ryzen KVM (RyzenKVM-2):** 1 shared core @ 3.5+ GHz, 2GB RAM, 30GB NVMe
- **$10/mo, EPYC VDS (EPYCVDS-1):** 1 **dedicated** EPYC Milan core, **8GB RAM**, 80GB NVMe

Same $10. The VDS gives you four times the RAM, five times the storage, double the bandwidth, and a core nobody else can use. Unless your budget is capped at $6/mo or you want the Ryzen single-thread clock for something bursty, the VDS-1 is the obvious pick at the $10 price point — that's rare; at most providers, dedicated-core plans start well above their shared plans' entry tier.

Year one, that's $120 for EPYCVDS-1. For the 8-core top plan, $80/mo buys 8 reserved Milan cores with 64GB RAM — a configuration that on bare metal typically means a full dedicated server rental. It's not a replacement for a dedicated server if you need the whole machine or custom hardware, but for pure CPU-reservation economics it undercuts most of the market.

One detail worth knowing before you click order: GreenCloud sells add-ons on the shared KVM lines at $3/1GB RAM, $3/CPU core, and $3/10GB SSD per month, **capped at doubling your existing configuration** — a 4GB VPS can take at most 4GB more RAM. You can't bolt your way from a Budget plan to a dedicated-core plan; reserved cores only come with the VDS line.

## Hidden limitations: APAC bandwidth, refunds, and promo fine print

Three things that live on GreenCloud's terms-of-service page and order notes rather than the pricing tables, but that should shape what you order:

**1. APAC locations get half the bandwidth.** Every line prices APAC locations (Singapore, Tokyo, Hong Kong, Vietnam) the same as US/EU but delivers roughly half the monthly transfer — EPYCVDS-1 is 4TB in US/EU, 2TB in APAC; RyzenKVM-1 is 1.5TB vs 750GB. Over committing is painful: extra bandwidth for KVM VPS costs $3/TB/mo in US/EU but $15/TB/mo in APAC. Heavy-transfer users should default to a US or EU location. GreenCloud is also explicit that bandwidth to China is best-effort unless "dedicated" appears in the product name, and recommends testing with their provided IPs before buying.

**2. Refunds are narrow.** New clients can request a refund within 7 days of registration, and only for their first VPS service. Crypto payments are non-refundable. Services that have used 10% or more of their allocated bandwidth don't qualify. Control panel add-ons (cPanel, DirectAdmin) are excluded. And critically, **promotional and flash-sale plans are marked "No refund / Money back on this plan"** — the Budget KVM line's sale plans carry this flag in the shopping cart too. If you order a promo plan, you're committing.

**3. Everything is unmanaged.** GreenCloud's terms state it plainly: "GreenCloud provides unmanaged services with hardware support for server functionality. Software support is limited to default installations selected during ordering." If you need someone else to configure your web stack, this isn't the right vendor at any plan level. Also note invoices go out 14 days before due date, late payments accrue a 10% fee after 2 days, and services can be suspended 1 day past due.

For readers in mainland China specifically: if your VPS IP gets blocked by the GFW within 3 hours of delivery, GreenCloud's terms allow one free IP change; otherwise it's $2.

## How GreenCloud's dedicated-core pricing compares

Since "vps with dedicated cores" is inherently a comparison search, here's the competitive context using verified figures. No links for the alternatives — if one of these fits better, search for it directly:

- **Contabo Max Performance VPS (VDS)** — 6 to 24 dedicated cores with 24–96GB RAM, positioned for SaaS platforms and production databases. Bigger floor than GreenCloud's line; no small 1–2 core entry option in this tier.
- **RackWorks dedicated CPU VPS** — pinned cores starting at $25/mo, with NUMA-local allocation as a stated feature. More expensive than GreenCloud's entry but explicitly engineered around cross-NUMA latency.
- **VPSLab** — Ryzen 9 9950X (Zen 5) plans with KVM-pinned cores and NVMe Gen4, aimed at single-thread performance. A different trade: fewer guaranteed cores, much higher per-core speed.
- **ServaRica VDS** — 2-core EPYC 7532 plans with 8GB RAM and 250–500GB NVMe, a budget dedicated-core option in the same spirit as GreenCloud's line.
- **RackNerd** — the perennial budget favorite (1GB KVM at $10.60/year during Black Friday 2025, per a third-party comparison), but its plans are conventional shared vCPUs on 1Gbps ports and don't advertise core reservation. Cheaper, yes; a dedicated-core answer, no.

The honest summary: if you want guaranteed cores under $15/mo, GreenCloud's EPYCVDS-1 at $10 is among the cheapest verifiable entry points, and its US/EU bandwidth allowances (4TB on a 10Gbps port) are generous for the price. If you need 6+ reserved cores with big RAM from day one, Contabo's tier is built for that. If single-thread speed matters more than core count, the pinned 9950X route is worth pricing out.

## Which plan should you actually pick?

A straightforward decision tree based on the verified numbers:

1. **CPU consistency matters and budget is tight** → EPYCVDS-1, $10/mo. 1 dedicated core, 8GB RAM. Skip the $6 shared plans entirely; the 8GB RAM difference alone justifies the extra $4.
2. **Need 2–4 dedicated cores** → EPYCVDS-2/3/4 ($20–40/mo). The scaling is linear: $10 per dedicated core per month, with RAM and NVMe bundled proportionally.
3. **8 reserved cores, 64GB RAM, under $100** → EPYCVDS-5 at $80/mo. Compare against dedicated server quotes before deciding, but for CPU-reservation purposes this is the value ceiling of the line.
4. **Bursty single-thread workloads, CPU guarantees irrelevant** → RyzenKVM-1 or -2 at $6–10/mo. The 3.5+ GHz clock is the selling point, not exclusivity.
5. **Absolute minimum spend, light sites and tinkering** → SSDKVM-1 at $6/mo.
6. **Windows required** → none of the above; the KVM lines are Linux-only, and you'd need GreenCloud's Hyper-V-based Windows VPS line (from $10/mo per third-party reviews) or another provider.

Two checks before checkout: confirm the location's bandwidth allowance matches your transfer needs (APAC halves it), and if you're ordering any promo-priced plan, assume it's non-refundable and pick the datacenter deliberately — location changes are free-ish ($3 one-time) between US/EU datacenters but restricted to same-country moves in APAC, and flash-sale plans can only change location after a month of activity, or not at all if a discount code was applied.

If reserved CPU is what brought you here, **👉 [grab GreenCloud's EPYC VDS dedicated-core plans starting at $10/mo](https://greencloudvps.com/billing/aff.php?aff=6679)** and start with the single-core plan — you can scale to 2, 3, 4 or 8 cores later, but you'll know within a week whether the $10 tier already covers your workload.

## FAQ

**Is a VDS with dedicated cores the same as a dedicated server?**
No. A VDS reserves specific physical cores and RAM for your VM, but the host machine is still shared with other VMs. A dedicated server is the entire physical machine. For CPU-predictability purposes they behave similarly; for disk I/O isolation, hardware control, and raw capacity, they don't.

**Does GreenCloud oversell its dedicated cores?**
The product page states 100% exclusive resources — dedicated physical cores, dedicated RAM, dedicated NVMe — for the EPYC VDS line. Independent verification of per-node occupancy isn't publicly available, which is true of every provider in this price class; the 7-day first-service refund is your practical safety net on standard plans (not promo plans).

**What happens if I exceed my bandwidth on a GreenCloud VPS?**
You can buy additional transfer: $3/TB/mo on US/EU locations, $15/TB/mo on APAC for KVM VPS. Since the first 10%+ of bandwidth use also voids refund eligibility, size your plan for realistic usage from day one.

**Can I upgrade a shared-core VPS into a dedicated-core VDS later?**
Not in place. The $3/core add-ons on Budget and Ryzen plans are capped at doubling your existing allocation and don't convert cores to dedicated. Moving up to the VDS line means ordering a new plan and migrating your data — plan for a maintenance window if you go that route.
