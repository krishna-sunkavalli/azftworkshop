# Contoso Outdoors Catalogue - Lab Data Package

Sample data for the GenAI Workshop, Session 1. Everything here is
fictional. Contoso Outdoors is not a real company and these products do
not exist.

## Contents

| Folder | Documents | Purpose |
|---|---|---|
| `products/` | 8 | Product specification sheets |
| `care/` | 4 | Care and maintenance guides |
| `policies/` | 5 | Returns, warranty, shipping, sizing, repairs |
| `pricing/` | 2 | Current and superseded price lists |
| root | 1 | Catalogue overview |

**20 documents to index**, plus this README, which is documentation about the package and is **not** part of the corpus.

> ⚠️ **Do not upload this file.** The tables below list the correct answers to the lab's test questions. Indexed alongside the catalogue it becomes an answer key the agent can quote — passing Exercise 4 while citing documents it never read. Upload the other **20** markdown files only.

## How the package is designed

This is not filler text. Specific properties are built in so the lab
exercises produce the intended results.

### Facts the agent must find

| Question | Answer | Source |
|---|---|---|
| Waterproof rating of the Summit 2P | Fly 1,500 mm HH, floor 5,000 mm HH | `products/summit-2p-tent.md` |
| Return window | 60 days from delivery | `policies/returns-policy.md` |
| Price of the Summit 2P | 429.00 USD | `pricing/price-list-2026.md` |

### Facts that are deliberately absent

The agent is instructed to abstain rather than guess. These have **no**
answer anywhere in the corpus, by design:

- Margins, unit costs, supplier terms
- Cryptocurrency payment policy
- Staff discount policy

Used by Exercise 3 Task 3.3 and Exercise 4 Task 4.4.

### The deliberate conflict

`pricing/price-list-2023-SUPERSEDED.md` gives the Summit 2P as
**349.00 USD**. `pricing/price-list-2026.md` gives **429.00 USD**.

Both are in the index. A naive agent quotes whichever chunk ranks
higher; a correctly instructed agent prefers the most recent effective
date and says so. This is the evaluation case in
Lab 2 Exercise 3.

### Near-miss retrieval

`products/cascade-rain-shell.md` also carries a waterproof rating, and a
much larger number (20,000 mm HH). A query about "waterproof rating"
that is not scoped to the tent may surface it. This is a retrieval
precision problem.

## Using the package

1. Upload the **20 markdown files** — everything except this README — to a Blob Storage container. Foundry does not host documents, it points a knowledge base at a system that already holds them.
2. Index the container with your `text-embed` deployment.
3. See [Lab 1 Exercise 3](../../Lab%201%20-%20Build%20your%20first%20Agent%20on%20Foundry/Exercise%203%20-%20Ground%20your%20agent%20with%20knowledge.md).

> Upload only the markdown files listed above. This README and the `inventory/` folder are both excluded — the inventory data is served separately, as a tool, see below.

## Inventory tool

`inventory/` backs the `check_inventory` tool built in [Lab 1 Exercise 4](../../Lab%201%20-%20Build%20your%20first%20Agent%20on%20Foundry/Exercise%204%20-%20Build%20and%20test%20your%20agent.md#task-44-add-a-tool-for-live-data):

| Path | What it is |
|---|---|
| `inventory/api/*.json` | **Eight per-SKU files you publish as blobs.** Each filename is a SKU, so `CO-TNT-S2P.json` is served at `…/inventory-api/CO-TNT-S2P.json` |
| `inventory/openapi-inventory.json` | The OpenAPI 3.0 description you paste into Foundry. **Edit `servers.url`** to your own storage account first |
| `inventory/inventory.json` | The same data as one file, for reading — not used by the tool |

Stock levels and lead times live here and **only** here — deliberately not in any catalogue document, so a stock question can only be answered by calling the tool. That is what makes a correct answer *proof* the tool ran.
