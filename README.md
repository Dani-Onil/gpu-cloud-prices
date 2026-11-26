# GPU cloud prices (open data)

Weekly on-demand GPU rental prices from GPU clouds (neoclouds), and the **GPU Price Index**: the typical price per GPU-hour for H100 SXM, H200, B200 and B300.

Collected by [bestneoclouds.com](https://bestneoclouds.com/gpu-price-index/) from each provider's public pricing page. Updated every Monday.

## Files

| File | What it has |
| --- | --- |
| `gpu-price-index.csv` | The index, one row per GPU per week |
| `gpu-prices.csv` | Every price we publish this week, one row per provider and GPU |
| `gpu-prices.json` | The same prices as JSON, with license, source and check date |

### gpu-price-index.csv

| Column | Meaning |
| --- | --- |
| `date` | Date of the weekly check (YYYY-MM-DD) |
| `gpu` | `H100 SXM`, `H200`, `B200` or `B300` |
| `median_usd_per_gpu_hour` | The index: median of each provider's lowest price, US dollars per GPU-hour |
| `providers` | How many providers are in the median |
| `low_usd_per_gpu_hour` | Lowest provider price that week |
| `high_usd_per_gpu_hour` | Highest provider price that week |

### gpu-prices.csv and gpu-prices.json

| Column | Meaning |
| --- | --- |
| `provider` | Provider name |
| `provider_slug` | Short ID, as in `https://bestneoclouds.com/providers/<slug>/` |
| `gpu` | GPU as the provider lists it (`H100 SXM`, `H100 PCIe`, `H200 NVL`, `B200`…) |
| `usd_per_gpu_hour` | Published price, US dollars per GPU-hour |
| `basis` | What the price is: on-demand, node size, billing, "marketplace", "from"… |
| `source_url` | The provider page the price was copied from |
| `checked` | Date of the check (YYYY-MM-DD) |

The price files include marketplace offers and "from" prices. The `basis` column says which they are.

## How the index is computed

1. Every Monday we open each provider's pricing page and copy its published on-demand prices.
2. For each GPU, we keep each provider's lowest fixed on-demand price. GPU names must match exactly: `H100 SXM` (not PCIe or NVL), `H200` (not H200 NVL), `B200`, `B300`.
3. We leave out marketplace offers, "from" prices and list prices with no capacity to deploy ("0 deployable").
4. The index is the median of those prices. With an even count, it is the average of the two middle prices.
5. A GPU gets a value only when 4 or more providers publish a price for it.

The median moves when a provider changes a price, and also when a provider adds or drops one. The `providers` column shows when that happens. The first weeks (from 2026-11-09) were rebuilt from the dated history of our data. Hyperscalers (AWS, Google Cloud, Azure) are not included.

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You can use, share and adapt the data, including for commercial work. Credit **bestneoclouds.com GPU Price Index** with a link to https://bestneoclouds.com/gpu-price-index/.

Prices are copied from public pages on the check date and can change at any time. Check the provider's page before you buy.

## Contact

Found a wrong price, or run a GPU cloud? Email editors@bestneoclouds.com with a link to the public pricing page.
