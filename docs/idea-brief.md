# Idea: Tissue Culture Profit Calculator

*Status: raw idea, second pass · 2026-10-12*

**Decided so far:** for hobbyists, a calculator (people pick a plant and get numbers), plus price tracking to show which plants have stable demand over time. Ferrous isn't doing tissue culture yet, so the tool doubles as a planning aid for picking a first plant.

## The one-liner
A website that takes a list of plants and, for each one, compares what the plant sells for against what it costs to clone it by tissue culture (TC), then shows the likely profit, how long it takes to get there, and how fast that profit will disappear.

That last part matters most. TC is the reason rare plants stop being rare: Monstera 'Thai Constellation' and Philodendron 'Pink Princess' went from hundreds of dollars to supermarket prices once labs scaled them. So the honest answer to "what's the profit from cloning X?" always comes with "for how long?" A tool that models that profit window is more useful than one that just divides price by cost.

## Who it's for
| Audience | What they want to know | Willingness to pay |
|---|---|---|
| Home / hobby TC growers (kitchen-lab, pressure cooker, still-air box) | "Which plant should I start in TC to pay for my hobby?" | Low to medium; big, enthusiastic audience |
| Small sellers on Etsy, eBay, Palmstreet, plant shows | "Should I buy a mother plant and clone it, or buy TC plugs wholesale?" | Medium |
| Small commercial labs and nurseries | "Which new lines are worth initiating, and when will the market saturate?" | High, but they already have spreadsheets and insider pricing |
| Collectors / buyers | "Is this $300 plant about to crash to $30?" | Low, but great traffic and SEO |

**Starting audience (decided):** hobbyists and small sellers. They have the question, lack the numbers, and are easy to reach (Reddit r/TissueCulture, r/RareHouseplants, Facebook groups, YouTube). Collectors come along for free via the "price crash" angle.

## How the cost model would work
The core is a cost per *sellable* plant, not per plantlet in a jar.

**Inputs per plant (with sensible defaults the user can override):**
1. **Initiation cost.** Getting a clean culture started from a mother plant: the mother plant itself, sterilization trials, failed attempts. Aroids are notoriously hard to clean up because of internal bacteria, so this can be several tries and months. Often the single biggest cost for a hobbyist.
2. **Multiplication rate.** How many shoots each one becomes per subculture cycle (e.g. 3x to 5x), and the cycle length (e.g. 4 to 8 weeks). Growth is exponential, so this drives everything.
3. **Media and consumables.** Agar, sugar, MS salts, hormones (BAP, NAA, etc.), PPM, jars, gloves, alcohol. Pennies per plantlet if you mix your own, more with premixed media.
4. **Labor.** Minutes per transfer. A trained commercial tech does a few thousand transfers a day; a hobbyist may do 50 to 200 in an evening. Usually the biggest ongoing cost, and the one hobbyists forget to count.
5. **Contamination loss.** Percent of vessels lost per cycle (roughly 1 to 5% commercial, 5 to 25% hobbyist).
6. **Rooting and acclimatization.** Moving plantlets out of the jar into soil, with a loss rate (often 10 to 30%) and weeks of humidity-tent time before they're sellable.
7. **Overhead.** Flow hood or still-air box, autoclave or pressure cooker, shelving, grow lights, electricity, spread across output.
8. **Sell-side costs.** Platform fees, shipping, heat/cold packs, unsellable runts.
9. **Genetic stability.** Some plants don't come true in TC. Many variegated cultivars are chimeras that revert or scramble (Monstera 'Albo' is the classic example). Somaclonal variation can show up in long-running lines. The model should flag a "true-to-type risk" per plant.

**Outputs:**
- Cost per sellable plant at a given scale (e.g. 100, 1,000, 10,000 plants).
- Time to first sale and time to N plants.
- Break-even point, and profit at today's price.
- **Profit under price decay:** apply a simple decay curve to the sale price (e.g. price halves every X months once the plant is widely in TC) and show cumulative profit. This turns "should I clone this?" into a real answer.

## Where price data could come from
- **eBay sold listings.** The best public signal of real sale prices. The official API for sold data is restricted, so it may mean manual sampling or a careful scraper (check terms).
- **Etsy, Palmstreet, Garden Goods Direct, Steve's Leaves, and similar shops.** Asking prices, not sale prices, but good for trends.
- **Facebook groups and plant shows.** Big part of the market but no data access. Could be crowdsourced via a "report a sale" form.
- **Wholesale TC lab catalogs.** Many labs (in the US, Thailand, Indonesia, Netherlands) publish plug or flask price lists to trade buyers. This gives the floor price once a plant is mass-produced, and is a strong signal that a crash is coming.
- **Google Trends** for demand and hype cycles.
- **Crowdsourced cost data.** Hobbyists sharing their actual multiplication and contamination rates per species would become a dataset nobody else has.

## Price tracking and stable demand
The calculator answers "is this profitable today?" Price tracking answers "will it still sell next year?" A plant with steady demand and a slowly falling price is a safer first project than one that's spiking.

**What to record.** Each observation is one row: plant, date, source, price, sold or just listed, and a size class (cutting, small rooted, medium, TC plug, flask). Size class matters most, because a 2-inch plug and a 6-inch pot of the same plant are different products and mixing them makes the chart meaningless.

**What to show per plant:**
- **Median sold price over time**, by size class, as a simple line or sparkline.
- **Sales volume:** how many sold per month. This is the real demand signal; price alone can stay high while nobody buys.
- **Sell-through:** sold versus listed. Many listings and few sales means supply is outrunning demand.
- **Listing count trend:** a fast rise in listings is usually the first sign that TC supply has arrived.
- **Price volatility:** how much the price swings month to month.
- **Wholesale availability:** the date a plant first shows up in TC lab catalogs, marked on the chart.
- **Search interest** from Google Trends, which has years of history for free and can fill in the past before our own tracking starts.

**Stability rating.** Combine the above into a simple label rather than a score nobody understands:
- **Steady:** volume holding or growing, low volatility, healthy sell-through. Good hobby candidate.
- **Rising:** volume and price climbing. Profit window open, but watch for TC supply.
- **Hype:** sharp spike in price or search interest, thin volume. Risky.
- **Saturating:** listings growing faster than sales, price sliding. Margin closing.

The calculator can then use the tracked trend as its price-decay assumption instead of a guessed slider.

**Start tracking early.** eBay only shows roughly the last 90 days of sold listings, so history can't be backfilled later. Logging even 20 plants weekly, starting now, builds a dataset that becomes the site's main advantage.

## Existing alternatives
- **Community price guides and spreadsheets** on Reddit and Facebook. Popular, but stale fast and price only, no cost side.
- **TC supply and education companies** (Plant Cell Technology, PhytoTech Labs, Kitchen Culture Kit style kits). They teach how to do TC, not whether it's worth it for a given plant.
- **Commercial labs' internal spreadsheets.** Exactly this model, but private.
- **Generic resale trackers** (eBay sold search, WorthPoint style tools). Prices only, no plant-specific context.

**Gap:** nobody puts market price, TC production cost, and saturation timing in one place. *(Inferred from general knowledge; worth a quick search before building.)*

## Legal issues to build in
*Not legal advice; this is the shape of the problem.*
- **US plant patents** cover asexual reproduction of a patented variety for 20 years. Tissue culture is asexual reproduction, so cloning a patented plant to sell (or even to give away) infringes without a license. Many named cultivars sold today carry a "PP" number or "PPAF" (patent applied for) on the tag.
- **Plant Variety Protection (PVP)** in the US mainly covers seed- and tuber-propagated plants. In the EU and many other countries, plant breeders' rights (e.g. Community Plant Variety Rights) cover propagating material however it's made.
- **Trademarks** on cultivar trade names can restrict how you label and sell a plant even after a patent expires.
- **CITES and import rules** matter for some genera (orchids, Nepenthes, some cacti and succulents). Flasked TC material is sometimes treated more leniently, but not always. Importing plant material into the US needs USDA APHIS permits.
- **Wild-collected species** may raise access-and-benefit-sharing issues (Nagoya Protocol) in the source country.

**What the site should do:** show a per-plant legal flag (patented / PBR protected / trademark / CITES / none known), link to the patent or PVP record when known, and say plainly "you can grow this for yourself, you may not be able to sell clones." This is also a real differentiator, since most hobbyists don't know it.

## Illustrative numbers
**Rough estimates only, from general knowledge as of 2026, not checked against current listings.** Retail is a typical small rooted plant from a hobby seller. TC plug is a typical wholesale price for a deflasked plantlet from a commercial lab. Cost is an estimated all-in production cost per sellable plant at hobby scale (a few hundred plants), including labor at a modest hourly rate.

| Plant | Retail (small, rooted) | Wholesale TC plug | Est. hobby cost per sellable plant | True-to-type risk | Market state |
|---|---|---|---|---|---|
| Monstera 'Thai Constellation' | $30 to $80 | $3 to $8 | $2 to $5 | Low (stable in TC) | Saturated; low margin |
| Philodendron 'Pink Princess' | $15 to $40 | $2 to $5 | $2 to $5 | Medium (variegation varies) | Saturated |
| Monstera 'Albo Borsigiana' | $80 to $250 (cutting) | Rarely available | n/a | High (chimera, reverts) | Not a TC candidate; cuttings only |
| Anthurium warocqueanum ('Queen') | $60 to $200 | $10 to $25 | $4 to $10 | Low | Still margin; slow grower |
| Philodendron 'Spiritus Sancti' | $100 to $300 | $15 to $40 | $5 to $12 | Low | Was thousands; falling fast |
| A newly released or hyped cultivar | $200+ | None yet | $10 to $30 + high initiation cost | Unknown | Biggest profit window, highest risk |

**What the table shows:** the margin per plant is still large on paper for most aroids, but the real money is in being early. Once a plant shows up in wholesale TC catalogs, retail tends to fall toward a few times the plug price within a year or two. The tool's best feature is a "how early are you?" signal.

## The smallest MVP
1. **A spreadsheet first.** One tab per plant with the cost inputs above and an output row, plus a shared price log tab: about 20 plants, recorded weekly from eBay sold listings, with size class. Test the calculator on 5 plants you know.
2. **Then a single static web page:** a dropdown of about 20 curated plants (popular aroids, Hoya, Alocasia, a few orchids), each with a manually updated price band and wholesale plug price, default cost inputs you can override, and outputs for cost per plant, break-even, and profit under price decay. Each plant also gets a price sparkline, monthly sales volume, and its stability rating (Steady, Rising, Hype, Saturating). Plus the legal and true-to-type flags.
3. **Keep the price log by hand** weekly for eBay and monthly for wholesale catalogs. No scraping or accounts until people actually use it.

Later: automated price collection, crowdsourced cost and price reports, alerts when a plant appears in wholesale catalogs, a "which plant should I start next?" ranking, and maybe a paid tier for small labs.

## Open questions
- Which 20 plants go in the first price log? Mix steady sellers (Hoya, common Anthurium, Alocasia) with hyped ones so the stability ratings have contrast.
- How many weekly observations does a plant need before its stability rating means anything? Probably at least 3 months.
- How do we get trustworthy sale prices without the eBay sold-data API?
- Can we get hobbyists to share real contamination and multiplication rates? That dataset could be the moat.
- How to present legal flags without implying legal advice, and how to keep patent status current.
- Does this pair with a content side (species-specific TC protocols, media recipes) to drive traffic?
- Monetization: affiliate links to TC supplies and wholesale labs, ads, or a pro tier?
