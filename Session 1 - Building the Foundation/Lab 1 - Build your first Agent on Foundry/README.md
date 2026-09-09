# 🧪 Hands-on Lab 1: Build your first Agent on Foundry

**⏱️ 11:10 – 12:00 (50 minutes)**

You are the architect on an approved pilot: the **Contoso Outdoor Gear Advisor** — an agent that answers customer product questions using only the approved catalogue, and tells the truth when it doesn't know.

In this lab you take it from an empty resource group to a working, grounded agent whose behaviour you can reproduce on demand.

---

## 🎯 Lab objectives

By the end of this lab you will have:

- ✅ A Foundry project in your own resource group
- ✅ A chat model and an embedding model deployed
- ✅ A knowledge source built from the Contoso catalogue
- ✅ A working agent with instructions, grounding and a tool
- ✅ A recorded behaviour baseline: grounded answers, tool calls and correct abstention

---

## 📚 Exercises

| # | Exercise | Time |
|---|---|---|
| 1 | [Provision your Foundry project](./Exercise%201%20-%20Provision%20your%20Foundry%20project.md) | 10m |
| 2 | [Deploy a model](./Exercise%202%20-%20Deploy%20a%20model.md) | 8m |
| 3 | [Ground your agent with knowledge](./Exercise%203%20-%20Ground%20your%20agent%20with%20knowledge.md) | 15m |
| 4 | [Build and test your agent](./Exercise%204%20-%20Build%20and%20test%20your%20agent.md) | 14m |

---

## 📋 Before you start

- [ ] You have completed the [**Prerequisites**](../Prerequisites.md) — in particular **User Access Administrator**, without which Exercise 3 cannot be finished
- [ ] You can sign in to the Azure portal with the account that holds your subscription
- [ ] Quota is approved in your lab region (see the [session pre-flight check](../README.md#-pre-flight-check))
- [ ] You have downloaded the **`contoso-outdoors-catalogue`** sample data package ([`lab-data/`](../lab-data/contoso-outdoors-catalogue/README.md))

### 🏷️ Naming convention

Replace `<initials>` with your own throughout. Keep it consistent — later exercises depend on these names.

| Resource | Name |
|---|---|
| Resource group | `rg-genai-workshop-<initials>` |
| Foundry project | `proj-gear-advisor-<initials>` |
| Chat deployment | `gpt-chat` |
| Embedding deployment | `text-embed` |
| Knowledge source | `contoso-catalogue` |
| Agent | `gear-advisor` |

> 💡 Using a fixed *deployment name* (`gpt-chat`) rather than the model's own name is deliberate — it lets you swap the underlying model later without touching the agent or any code. This is the swap-ability principle in action.

---

## 🆘 If you get stuck

| Symptom | Most likely cause |
|---|---|
| Model not listed / cannot deploy | No quota in this region — try your fallback region |
| Deployment stuck "Creating" | Regional capacity; pick a different model tier |
| "This region is at capacity" creating AI Search | Genuinely full — pick another region; it need not match the project |
| **"Failed to fetch knowledge bases for connection…"** | Search service is API-key-only; set `--auth-options aadOrApiKey`, or use a Foundry-created resource |
| **Indexer won't create: "Unable to retrieve blob container"** | BYO search service identity lacks **Storage Blob Data Reader** on the storage account |
| Agent errors with **403 Forbidden** on `…/mcp` | Foundry identities lack **Search Index Data Reader** on the search service |
| Agent errors with **502** *"failed to authenticate to the vectorization endpoint"* | Search service identity is off, or lacks **Cognitive Services User** on the Foundry resource |
| Agent answers with no citations | Knowledge base not attached, or indexing not finished |
| **Agent abstains on everything, suddenly** | Config was not **saved** — knowledge attachment or instructions silently reverted. Refresh and check the version number |
| **Agent abstains on one prompt mid-conversation** | An earlier abstention in the same thread suppresses retrieval — start a **new chat** |
| "I don't know" to everything | Indexing incomplete, or the wrong embedding deployment is bound |
| Agent answers from the open web | The **Web search** tool is attached by default — remove it **and save** |
| **Agent is using a model you didn't deploy** | New agents default to the portal's current model and auto-create that deployment — set it back to `gpt-chat` |
| Portal blade looks different | The product UI moves fast — follow the *intent* of the step, not the pixel |

Raise a hand rather than burning 10 minutes. The lab is timeboxed.

---

**Start here ▶️ [Exercise 1 — Provision your Foundry project](./Exercise%201%20-%20Provision%20your%20Foundry%20project.md)**
