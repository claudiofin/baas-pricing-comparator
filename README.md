# BaaS Pricing Comparator — Cloudflare vs Supabase vs Firebase vs Convex

An interactive, single-file HTML tool that estimates and compares the monthly bill of four backend-as-a-service / serverless stacks — **Cloudflare** (Workers + D1 + R2 + Durable Objects), **Supabase**, **Firebase** (Blaze), and **Convex** — for the *same* application workload.

🔗 No build step, no dependencies, no server: open `comparatore-prezzi-cloud.html` in any browser, or drop it on any static host. Works fully offline (the only external links are two clickable source citations).

🌍 Available in **Italian** and **English** (toggle top-right; the choice is remembered).

## What it does

Set your workload once — monthly active users, database reads/writes/storage, file storage/egress, function invocations/duration/memory, realtime connections/messages — and the tool computes, side by side:

- **Direct cost comparison** — total monthly bill per provider, broken down line by line by billing category (base plan, database, storage & bandwidth, compute, realtime, auth).
- **Scenario presets** — hobby project, growing SaaS, realtime-heavy app, content-heavy e-commerce, high-traffic B2B API — to set every input at once.
- **Provider-specific extras** — Cloudflare Workers AI / Workers for Platforms, a forceable Supabase plan (Free/Pro/Team), Firebase App Hosting bandwidth, Convex developer-seat count and plan.
- **Scaling / crossover chart** — sweeps one dimension (e.g. MAU) from zero to its maximum while holding the others fixed, and finds the exact points where one provider becomes cheaper than another (via bisection against the real, piecewise cost functions — not linear interpolation, since free-tier cliffs would throw that off).
- **Unit economics** — cost per 1,000 MAU, cost per million requests, and margin at the price you charge your own customers.

## Why

Cloud pricing pages are marketing content, not APIs. Comparing four providers' free tiers, overage rates, and billing quirks (e.g. Cloudflare never bills egress; Convex's reactive queries are compute-free but Actions aren't; Firebase Cloud Functions bills full wall-clock time while Cloudflare Workers excludes I/O wait) by hand is slow and error-prone. This tool encodes those rules once, so changing one slider recomputes all four honestly — including provider-specific quirks that a naive per-request or per-GB comparison would miss.

## Methodology & limitations

Every pricing rule is documented **inside the tool itself** (bottom section, "Methodology & limitations" / "Metodologia e limiti"), including:
- exactly what's modeled per provider and what isn't (add-ons, multi-region, text/vector search, local taxes, etc.)
- every simplification/assumption, each traceable to a specific input or formula
- sources: official docs (verified live via MCP for Cloudflare and Supabase; via direct fetch/official pricing pages for Firebase and Convex), with an "estimate" flag on anything triangulated rather than directly confirmed

**This is an estimation tool to get your bearings, not an invoice.** Always recheck with the provider's official calculator before deciding.

## Verified

Pricing verified July 2026. Currency: USD, excl. VAT. Rerun the checks yourself against:
- developers.cloudflare.com/workers/platform/pricing, /d1/platform/pricing, /r2/pricing, /durable-objects/platform/pricing
- supabase.com/docs/guides/platform/billing-on-supabase
- firebase.google.com/pricing
- convex.dev/pricing

## License

MIT — see [LICENSE](LICENSE).
