# residential ip provider: How to Compare Per-IP and Per-GB Pricing Without Overpaying

Two different people type "residential ip provider" into Google, and they need opposite things.

One runs a scraper that burns hundreds of gigabytes a month through a handful of addresses and is tired of watching a data counter. The other needs thousands of distinct exit IPs a day, each carrying tiny payloads, and doesn't care which address serves which request. Both get shown the same comparison tables, usually led by a per-GB rate. That number is meaningless for the first person and essential for the second.

So before any provider recommendation, it's worth getting the billing unit right. Everything else — pool size claims, protocol support, dashboard polish — is secondary to whether you're being charged for the thing you actually consume.

## The three products hiding behind one search term

Most "residential proxy" shopping pages blur together three products that are billed differently:

**Rotating residential bandwidth.** You pay per gigabyte. Every request can come out of a different address from a shared pool. Expensive per unit, and it's the right buy when your work is rotation-heavy and low-bandwidth per request — geo-checking, ad verification, lightweight SERP pulls, API polling.

**Per-IP residential access.** You buy a number of addresses and hold them for a session. The address is yours until it goes offline, and traffic is typically unmetered. This is what you want for logged-in sessions, cart flows, multi-account work, and any pipeline where you'd rather not think about bandwidth.

**Static residential / ISP proxies.** Addresses registered to consumer ISPs but hosted in a datacenter. Fixed for a billing period, faster, and a different product category entirely. Most providers price these per IP per month, and you can't compare them to a per-GB rate at all.

Comparing a per-GB quote against a per-IP quote is like comparing a taxi fare to a rental car. The units aren't the same thing, and the cheaper-looking one usually wins only because it's measuring less.

9Proxy's whole pitch sits on the second model: pay per address, bandwidth included. Whether that's cheaper for you is a workload question, not a marketing question. Here's the arithmetic.

## Worked examples: where per-IP wins and where it loses

Two scenarios, using 9Proxy's currently published rates (smallest IP package is 100 addresses for $24 with unlimited bandwidth; the GB packs run from 5 GB at $15 down to roughly $0.75/GB at the 2,000 GB tier).

**Scenario A — 600 GB a month across ~20 addresses on one target.** On the per-IP side, a single 100-IP package at $24 covers the whole month, because bandwidth isn't metered and 100 addresses is more than the 20 you're using in parallel. On the per-GB side, 600 GB at the $1.00/GB rate works out to $600 of traffic — and since those GB packs are one-off purchases with 180-day validity rather than monthly subscriptions, you'd be re-buying packs the following month. That's roughly a 25× gap for identical output.

**Scenario B — 30 GB a month rotated across thousands of exits.** Now the per-IP model fights itself. On IP-based plans, one address equals one use when you forward through it, so rotating across thousands of exits means buying thousands of addresses — 5,000 IPs runs $360. On the per-GB side, the 50 GB pack at $105 covers a month of work with room to spare, and you can generate as many endpoints as you want inside that traffic. Per-GB wins by a wide margin.

Same provider, same network, opposite answer. If you can't say which of those two shapes your workload has, no comparison table is going to help you, and any provider that pushes a single headline rate is selling you a guess.

> The 180-day validity on 9Proxy's GB packs matters more than it looks. Monthly-expiring traffic forces you to buy for your peak month even when usage is lumpy.

## What to check before you hand over card details

Price is the easy part of this decision. The harder parts are the ones that don't appear in a pricing table.

**Where the pool comes from.** This stopped being a philosophical question. In June 2026, a scan of 6,038 smart-TV apps found proxy SDKs in 2,058 of them, still proxying after the app was closed, and in July 2026 the FBI seized a residential proxy provider's domains over an alleged botnet of roughly two million devices whose owners never consented. Providers that pay participants and keep consent records carry real costs; a price far below market either reflects genuine scale or reflects a cost that isn't being paid. Ask the question and see what the answer sounds like.

**Traffic expiry.** Watch for monthly resets versus long validity windows. It won't show up on a comparison table and it will show up on your invoice.

**Billed failures.** Blocked responses, redirects, error pages and CAPTCHA interstitials all transfer data. On a metered plan, you pay for the request that failed. A 20% failure rate is 20% extra traffic for nothing.

**Minimum purchase size.** Plenty of providers quote "$0.015/IP" and then require a five-figure order to reach it. Look at what you pay at your actual volume, not at the tier that unlocks the headline rate.

**Self-reported pool numbers.** Every "20M+ IPs" or "100M+ IPs" figure in this category is vendor-stated and unaudited. Exit-node freshness and rotation logic matter more in production than the advertised size of the pool.

9Proxy's own documentation describes the network as real residential devices and lists 20M+ addresses across 90+ countries. On the sourcing question specifically, the public materials I could check don't name a participant-compensation or opt-in program the way some larger providers do — if that's a deciding factor for your use case, raise it with support before you buy rather than after. It's a fair question to ask any provider in this category, and the willingness to answer tells you something useful on its own.

## How 9Proxy's two models actually differ

This is the part that gets glossed over in most roundups. The two products don't just bill differently — they behave differently at the technical level.

|  | Residential by IPs | Residential by GB |
| --- | --- | --- |
| Billing unit | Fixed package, by address count | Fixed package, by total GB |
| Traffic | Unlimited while the IP is active | Capped by purchased GB |
| Usage window | Until all IPs are consumed; unused IPs don't expire | 180 days (unlimited on Enterprise) |
| Address lifespan | A few hours up to ~24h, varies per IP | Rotates per request or per sticky session |
| Endpoint generation | 1 IP = 1 use when forwarded | Unlimited endpoints, only GB deducted |
| Rotation control | Via Auto Rotation Proxy on selected ports | Rotating or sticky mode, configurable |
| Authentication | Desktop app with local port forwarding, optional proxy auth | Username/password or IP whitelist, no app needed |
| Targeting | Country, city, ISP, ZIP filters in the app | Country, state, city, ZIP, ISP in the dashboard |

The practical consequence: the GB product runs entirely from the browser dashboard, which is convenient for cloud jobs and scripts. The IP product depends on a desktop application. Reviewers have flagged that dependency as the main friction point for multi-device setups, so plan accordingly if you work across several machines.

Both sides support HTTP/HTTPS and SOCKS5, which matters more than it sounds — SOCKS5 is what you need for tools like Playwright, Puppeteer and Scrapy that pass non-HTTP traffic or hold long-lived connections.

## The full plan lineup

9Proxy raised prices on its IP-based and bundle packages on June 1, 2026 — the first adjustment the company says it has made — while leaving GB-based pricing untouched. The figures below reflect the post-adjustment structure as it appears in current reviews and vendor documentation. Rates at promotional tiers move, so confirm before you commit.

### IP-based residential packages (unlimited bandwidth per IP)

| Package | Effective rate | Total | Best for | Buy |
| --- | --- | --- | --- | --- |
| 100 IPs | $0.24/IP | $24 | Proof of concept, small jobs | [Start with the 100 IP package](https://bit.ly/9-Proxy) |
| 500 IPs | $0.144/IP | $72 | Solo operators, light scraping, multi-account work | [Compare the 500 IP tier](https://bit.ly/9-Proxy) |
| 1,000 IPs + 500 bonus | $0.084/IP | $126 | Steady workloads, small teams (vendor's most popular tier) | [Check the 1,000 + 500 IP package](https://bit.ly/9-Proxy) |
| 2,500 IPs | $0.084/IP | $210 | Several verticals running in parallel | [See pricing for 2,500 IPs](https://bit.ly/9-Proxy) |
| 5,000 IPs | $0.072/IP | $360 | Agencies, mid-scale price and SERP stacks | [Look at the 5,000 IP package](https://bit.ly/9-Proxy) |
| 15,000 IPs | $0.048/IP | $720 | Regional teams with ongoing pipelines | [Review the 15,000 IP tier](https://bit.ly/9-Proxy) |
| 25,000 IPs | $0.035/IP | $863 | Heavy automation, reseller inventory | [Get the 25,000 IP package](https://bit.ly/9-Proxy) |
| 50,000 IPs | $0.029/IP | $1,438 | High-volume resellers, platform-level operations | [Check the 50,000 IP tier](https://bit.ly/9-Proxy) |
| 100,000 IPs (Business) | $0.023/IP | $2,300 | Industrial-scale collection | [Ask about high-volume IP pricing](https://bit.ly/9-Proxy) |
| 200,000 IPs (Business) | $0.021/IP | $4,140 | Enterprise pipelines | [Enquire about the 200,000 IP package](https://bit.ly/9-Proxy) |
| 500,000 IPs (Business) | $0.018/IP | $8,625 | Reseller-scale inventory | [See the largest IP package](https://bit.ly/9-Proxy) |

### GB-based residential packages (rotating endpoints)

| Package | Rate | Total | Validity | Buy |
| --- | --- | --- | --- | --- |
| 5 GB | $3.00/GB | $15 | 180 days | [Buy the 5 GB starter pack](https://bit.ly/9-Proxy) |
| 50 GB + 5 GB bonus | $2.10/GB | $105 | 180 days | [Get the 50 GB + 5 GB pack](https://bit.ly/9-Proxy) |
| 100 GB | $1.50/GB | $150 | 180 days | [Check the 100 GB package](https://bit.ly/9-Proxy) |
| 200 GB | $1.00/GB | $200 | 180 days | [Buy the 200 GB pack](https://bit.ly/9-Proxy) |
| 1,000 GB | $0.80/GB | $800 | 180 days | [See the 1,000 GB tier](https://bit.ly/9-Proxy) |
| 2,000 GB | $0.75/GB | $1,500 | 180 days | [Compare the 2,000 GB package](https://bit.ly/9-Proxy) |

The advertised floor on the GB side is $0.68/GB at the highest committed volume. Note the ceiling on the entry pack: at $3.00/GB, the 5 GB bundle is a testing purchase, not a working one. If you already know your monthly burn, buying 5 GB at a time is the expensive way to find out.

### Bundle packages (IPs plus traffic)

| Bundle | Contents | Price | Buy |
| --- | --- | --- | --- |
| Starter | 100 IPs + 5 GB | $30 | [Get the Starter bundle](https://bit.ly/9-Proxy) |
| Popular | 1,500 IPs + 50 GB | $180 | [Check the Popular bundle](https://bit.ly/9-Proxy) |
| Pro | 5,000 IPs + 500 GB | $720 | [See the Pro bundle pricing](https://bit.ly/9-Proxy) |

The Pro bundle lists at $860 against a $720 discounted price, a 16.28% reduction, according to 9Proxy's own billing documentation. Bundled traffic carries the same 180-day validity as standalone GB packs.

### Enterprise

Pricing is quoted rather than published. What's documented: unlimited data validity, team mode for one owner plus up to five members, per-member traffic controls, activity logs, unlimited share-code creation, no expiration on traffic shared inside the team, and dedicated support. If you're an agency billing clients or running an always-on pipeline, that's the conversation to have, and it's the only tier where the traffic-validity constraint disappears.

👉 [Request Enterprise pricing and plan details](https://bit.ly/9-Proxy)

## Matching a plan to a real workload

Short version, based on the billing mechanics rather than on the tier names:

- **Testing whether residential IPs solve your problem at all** — 5 GB at $15 if your traffic is rotation-heavy, or the 100-IP package at $24 if you need stable sessions. Both are cheap enough to be a real test rather than a commitment.
- **Daily rank tracking or price monitoring with moderate volume** — the 50 GB pack, or a 100–500 IP package if your sessions need to persist.
- **Multi-account management with an anti-detect browser** — per-IP packages. Each profile wants its own consistent address, and unmetered bandwidth removes the counter-watching entirely.
- **High-volume scraping where pages are heavy and bandwidth is unpredictable** — per-IP, scaling to the 5,000 or 15,000 tier. Paying per gigabyte for 2–5 MB rendered pages is how proxy bills reach four figures.
- **Bursty, seasonal, or client-project work** — GB packs. The 180-day validity means an idle month doesn't burn your balance.

## Operational details that decide whether it works day to day

A few specifics worth knowing before purchase, because they shape how the network behaves in production.

Residential IPs die. That's true of every provider in this category, and the useful question is what happens when they do. 9Proxy's documented answer is a 60-second replacement policy — addresses that fail to connect within the first minute are replaced — plus an Auto Refresh function that swaps offline ports automatically. The Today List lets you reuse any address you've touched in the last 24 hours at no extra cost if it comes back online, which is where the vendor's own cost-saving estimate of roughly 20–30% comes from for recurring jobs.

Address lifespan on the IP side runs from a few hours up to about 24 hours, and it varies. If your workflow needs the same address alive for a week, this is the wrong product category — you want static residential or ISP proxies, which 9Proxy lists as coming soon rather than available.

Authentication splits by model: user/password or IP whitelisting on the GB side with sub-user accounts, and the desktop app with optional proxy authentication on the IP side. Payments cover cards, crypto (USDT, BTC, ETH, LTC, DOGE and others), bank cards, Alipay, Apple Pay and Google Pay.

Trials exist but aren't guaranteed — availability is limited and typically arranged through support rather than self-serve. Ask before assuming you can test for free.

## What independent reviews report

Worth separating what's measured from what's claimed. The vendor states 99.95% uptime. Third-party numbers look like this:

Geekflare's 2026 review treats the network as still competitive after the price adjustment, noting the unlimited-bandwidth model as the main differentiator for bandwidth-unpredictable workloads. ProxyLook's comparison directory scores it 3.9/5 with a 7.8/10 trust score and lists a 97% success rate against an average response time of around 1,300 ms. Multilogin, which bundles the service alongside its own anti-detect browser, cites a 92–97% success rate and sub-second average response times. iTWire's review measured throughput in the 50–100 Mbps range with uptime near 99%, while flagging that streaming services like Netflix may still detect it and that the mandatory app complicates multi-device use. A longer independent test published by ProxyBros reported roughly 99.5% success and 0.6-second average responses over a month of running ~12M requests.

One user review on AlternativeTo mentions stable residential IPs and workable integration with Dolphin Anty and AdsPower. That's a single data point, not a consensus, but it aligns with the anti-detect browser use case the per-IP model is built for.

The honest read: per-IP with unlimited bandwidth is a genuinely different economic proposition from metered residential, and the trade is that addresses are shorter-lived and the IP product requires a desktop app in the loop.

## Getting started

The sign-up flow is three steps: create an account, buy a package, choose your access method — desktop app for full control, or the browser dashboard if you're on the GB model and want to generate endpoints immediately. Third-party integration via SOCKS5 works with anti-detect browsers, proxychains and custom scripts without protocol conversion.

The link below carries an invite code; 9Proxy lists a 5% discount for referred users, so it's worth using rather than signing up cold.

👉 [Create a 9Proxy account and see current residential IP pricing](https://bit.ly/9-Proxy)

If you're still undecided between the two models, buy the smallest package on the side that matches your workload's shape — $15 or $24 — and run it against your actual targets for a week. A benchmark on your own site mix at your own concurrency tells you more than any comparison table, including this one.
