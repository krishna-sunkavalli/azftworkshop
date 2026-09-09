# Session 1 — 🏗️ Building the Foundation

Build a grounded agent on Microsoft Foundry, then make it defensible: hardened identity, enforced guardrails, a measured quality baseline, live telemetry and a real cost model.

Two labs, nine exercises, roughly two hours at your own pace.

---

## 🧪 Labs

| # | Lab | What you build | Time |
|---|---|---|---|
| 1 | [Build your first Agent on Foundry](./Lab%201%20-%20Build%20your%20first%20Agent%20on%20Foundry/README.md) | A Foundry project, two model deployments, a grounded knowledge base, and an agent that cites its sources and abstains when it should | ~50m |
| 2 | [Secure, evaluate & monitor your first agent](./Lab%202%20-%20Secure,%20evaluate%20&%20monitor%20your%20first%20agent/README.md) | Identity and network hardening, guardrails, an evaluation run, traces you can read, and cost per conversation | ~50m |

Do them in order — Lab 2 hardens the agent Lab 1 builds.

---

## 🛫 Pre-flight check

Everything you need before starting is in the [**Prerequisites**](./Prerequisites.md) — quota, Azure AI Search capacity, RBAC, resource providers and network access.

Work through it **first**. Two items have 24–48 hour lead times:

- **Model quota** — ≥ 30K TPM for a chat *and* an embedding model, in your chosen region
- **Azure AI Search capacity** — test creating one, and pick a fallback region

The single most common cause of Lab 1 failing is missing **User Access Administrator**, and it bites late — after you have spent twenty minutes building things that look fine.

---

## 🧰 Ground rules

- **Nothing real goes in.** Sample data only — never customer or production data.
- **Read the callouts.** The ⚠️ and 🔑 notes exist because something actually failed there.
- **Screenshots drift.** Where a screenshot and the portal disagree, trust the portal.

---

## 🧹 Clean-up

When you are finished, delete the resource group:

```bash
az group delete --name rg-genai-workshop-<yourinitials> --yes --no-wait
```

> ⚠️ **Delete the resource group even if you keep nothing else.** Standard (pay-as-you-go) model deployments do not accrue when unused, but **storage and Azure AI Search do**. Check which Search SKU you were given — a provisioned **Standard S1** bills **$0.34/hour whether or not anyone queries it** (~$248/month), while **serverless** bills on use. Verify with:
>
> ```bash
> az search service show --resource-group rg-genai-workshop-<yourinitials> --name <search-service> --query sku
> ```

> 🔑 **Deleting the resource group is not always enough.** Foundry resources are **soft-deleted** and keep holding their name and quota allocation. List them with `az cognitiveservices account list-deleted`, and purge with `az cognitiveservices account purge --location <region> --resource-group <rg> --name <name>`.
