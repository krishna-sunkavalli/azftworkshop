# 🖼️ Media

Screenshots referenced by the lab exercises live here.

## Naming convention

```
media/s1-lab<lab#>-ex<exercise#>-<step#>.png
```

Examples:

| File | Used by |
|---|---|
| `s1-lab1-ex1-01.png` | Session 1 → Lab 1 → Exercise 1 → Step 1 |
| `s1-lab2-ex3-06.png` | Session 1 → Lab 2 → Exercise 3 → Step 6 |

## When to include a screenshot

A screenshot earns its place only when it shows something the written
step cannot. Use one when the reader needs to see:

1. **A completed form** — what correct input actually looks like, when
   several fields interact or one is easy to get wrong.
2. **A result or status** — proof the step worked, especially when the
   next step depends on it.
3. **A non-obvious location or choice** — where something lives when it
   is genuinely hard to find, or a decision point whose options are not
   self-evident from the text.

## When to leave it out

Do **not** add a screenshot for:

- Clicking a clearly named button — *Save*, *Next*, *Create*, *Deploy*
- Sign-in and landing pages
- A screen already shown a step or two earlier
- Progress spinners
- Anything the sentence already describes completely

> The test: **remove the image and re-read the step.** If it is still
> unambiguous, the image was decoration.

An exercise with a picture of every click is harder to follow, not
easier — the reader scrolls past screenshots to find the instruction,
and every image is one more thing to re-capture when the portal
changes. Target roughly **4–7 images per exercise**.

## Capture guidance

- Capture at **1440×900**. Full viewport is fine; crop only when the
  relevant panel is a small part of a busy screen.
- Capture in a **lab or demo tenant** — never a production or corporate
  one. Screenshots bake in subscription names, resource IDs and user
  principal names.
- **Redact** anything that survives from a real tenant: subscription
  IDs, tenant IDs, customer names, email addresses.
- Draw call-outs in a single accent colour (orange `#F25022`) so the
  deck and the lab match.
- Save as PNG. Keep each file under ~400 KB so the repo stays
  clone-friendly.

> Exercise steps reference these paths directly. Drop the matching PNG
> in and the image renders with no edit to the markdown.
