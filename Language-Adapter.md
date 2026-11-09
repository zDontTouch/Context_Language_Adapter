---
name: context-language-adapter
description: >-
  Adapts a user's text to match the communication style expected by a target customer's cultural background — either high-context (descriptive, relational, rich in examples and analogies) or low-context (direct, concise, factual). Activate when the user includes "context-adapter" in their message followed by the text to adapt. The skill asks for the target customer's nationality or a direct High-Context / Low-Context preference, then rewrites the content accordingly. Trigger phrases include: "context-adapter", "context adapter", "/context-adapter".
metadata:
  author: Leonardo Felini
  version: 2.3.1
  tags: communication culture customer localization high-context low-context
---

# Context Language Adapter

This skill rewrites any text to match the communication style expected by a target customer's cultural background, using Hofstede's cultural dimensions for nuanced adaptation — beyond a simple High/Low classification.

---

## Cultural Context Framework

Every culture develops a default way of packaging meaning. In high-context cultures, most of the message is carried by the situation: shared history, relationships, non-verbal signals, and unwritten rules. In low-context cultures, the message is carried almost entirely by the words themselves.

### High-Context Cultures

Meaning is implicit. People rely on long-standing relationships and shared understanding, so messages are dense with what everyone already knows.

- Indirect, nuanced, and relationship-first communication
- Strong emphasis on saving face and preserving harmony
- Non-verbal cues, silence, and timing carry real meaning
- Trust in relationships matters more than written contracts
- Meaning lives in situation, relationship, and shared history
- Communication is indirect and layered with implication
- Silence is meaningful and can be a complete answer
- Status and seniority shape who speaks and who decides
- Long-term relationships gate business, trust, and information
- **Avoid**: Cold, overly blunt phrasing that ignores the relationship or suggests a lack of trust

### Low-Context Cultures

Meaning is explicit. People spell things out in detail because little is assumed about shared context. Clarity and efficiency take priority.

- Direct, precise, and text-focused communication
- Agreements and expectations written down
- Punctuality, agendas, and structured meetings
- Conflict handled openly and quickly
- Meaning is carried mainly by words and documents
- Communication is direct, precise, and action-oriented
- Silence signals a gap, a refusal, or a need for more detail
- Anyone may speak, and ideas are judged on their own merit
- Contracts and procedures replace reliance on relationships
- **Avoid**: Vague wording, implied expectations, and unstated assumptions

> **Important**: These are tendencies, not scripts. A pragmatic professional from a high-context culture can be extremely direct, and a relationship-focused person from a low-context culture can be deeply attuned to nuance. Every individual sits somewhere on the spectrum.

---

## Hofstede Dimension Guide

Use these six dimensions to layer nuance on top of the base High/Low style. Scores range roughly 0–120. Values marked **?** are uncertain — skip that dimension's nuance.

### PDI — Power Distance Index: Where Authority Matters Most

Measures how societies handle inequality and hierarchy. High PDI scores indicate strong acceptance of hierarchical order; low scores reflect societies that strive for equality.

- **PDI > 60**: Use formal salutation; acknowledge the recipient's role or seniority; avoid phrasing that could feel like a direct challenge or criticism
- **PDI < 40**: Egalitarian and approachable tone; first names acceptable; flat, non-hierarchical language
- **PDI 40–60** (no rule triggered): Measures acceptance of hierarchy and unequal distribution of power in society

### IDV — Individualism vs Collectivism: The I vs We Dimension

Measures how integrated individuals are into groups. High individualism means people primarily care for themselves and their immediate family; low individualism (collectivism) reflects strong group loyalty and interdependence.

- **IDV > 60** (Individualist): Use "you" framing; highlight personal benefit and individual empowerment; direct appeal to the reader's own interest
- **IDV < 40** (Collectivist): Use "we" and "our team" framing; emphasise group benefit, shared harmony, and collective outcome
- **IDV 40–60** (no rule triggered): Measures the degree to which individuals act independently vs. as part of a group

### MAS — Masculinity vs Femininity: Society's Emotional Roles

Distinguishes between assertive, competitive masculine cultures and modest, nurturing feminine cultures. High MAS societies value achievement and success; low MAS societies value care, quality of life, and consensus.

- **MAS > 60**: Results-focused and assertive language; lead with outcomes and achievements
- **MAS < 40**: Collaborative and consensus-seeking language; emphasise shared success, mutual care, and quality of experience
- **MAS 40–60** (no rule triggered): Measures the distribution between assertive, competitive values and nurturing, collaborative values in society

### UAI — Uncertainty Avoidance Index: Managing the Unknown

High UAI societies feel threatened by ambiguity and require structure, rules, and detailed guidance. Low UAI societies are comfortable with uncertainty and unstructured situations.

- **UAI > 70**: Provide clear, step-by-step structure; eliminate ambiguity; state every assumption and expectation explicitly
- **UAI < 40**: Concise and flexible; broad strokes are acceptable; no need for exhaustive procedural detail
- **UAI 40–70** (no rule triggered): Measures tolerance for ambiguity and the need for rules and predictable structure

### LTO — Long-Term vs Short-Term Orientation: Future vs Present Focus

Measures whether a society values future rewards — such as perseverance and thrift — or past and present priorities such as tradition and social obligations.

- **LTO > 60**: Emphasise long-term reliability, relationship continuity, and future benefits; frame the solution as an investment
- **LTO < 30**: Emphasise immediate resolution, quick wins, and concrete near-term outcomes; appeal to tradition or established norms where relevant
- **LTO 30–60** (no rule triggered): Measures whether a society values future rewards or present and tradition-based priorities

### IVR — Indulgence vs Restraint: Enjoying Life vs Self-Regulation

Measures whether societies allow free gratification of basic desires and enjoyment of life, or regulate them through strict social norms and expectations.

- **IVR > 60**: Warmer and more expressive tone; positive, upbeat closing; some informality is welcome
- **IVR < 35**: Measured and formal tone; restrained emotional expression; avoid casual or overly cheerful phrasing
- **IVR 35–60** (no rule triggered): Measures the degree to which societies allow free gratification of desires vs. regulation through strict norms

---

## Regional Cultural Clusters

When a country belongs to one of the clusters below, use the cluster's Key Insight as additional context to enrich the adaptation — on top of the individual country's dimension values.

### The Nordic Cluster
*Denmark, Finland, Sweden, Norway, Iceland*

The Nordic countries share similar cultural profiles that reflect strong welfare states and consensus-based societies.

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 19 | Exceptionally low power distance; citizens expect equality and participative decision-making |
| IDV | 69 | Strong individualism; personal responsibility and self-reliance |
| MAS | 25 | Strong femininity; focus on quality of life, cooperation, and gender equality |
| UAI | 40 | Low uncertainty avoidance; tolerant of ambiguity; pragmatic approach |
| LTO | 45 | Moderate long-term orientation; balanced focus on tradition and future |
| IVR | 60 | High indulgence; emphasis on happiness, leisure, and life satisfaction |

**Key Insight**: Nordic societies are characterised by egalitarianism, social welfare, work-life balance, and consensus-driven decision-making. These patterns reflect feminine cultural values that prioritise care and quality of life. Write as a peer, not an authority. Avoid hierarchy signals and emphasise shared benefit and openness.

---

### The Anglo Cluster
*United States, Canada, Australia, New Zealand, Great Britain, Ireland*

English-speaking countries share cultural roots that emphasise individualism and personal achievement.

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 38 | Low power distance; people question authority and expect equal rights |
| IDV | 83 | Very high individualism; emphasis on personal freedom, self-reliance, and individual rights |
| MAS | 58 | High masculinity; focus on competition, achievement, and material success |
| UAI | 42 | Low uncertainty avoidance; tolerance for ambiguity and risk-taking |
| LTO | 29 | Short-term orientation; focus on tradition, quick results, and social obligations |
| IVR | 67 | High indulgence; emphasis on enjoying life, freedom of choice, and personal happiness |

**Key Insight**: Anglo cultures prioritise individual freedom, personal achievement, and meritocracy. Their tolerance for ambiguity and emphasis on personal initiative support direct, confident communication. Lead with the outcome and frame it around what the individual gains.

---

### The Five Dragons
*Japan, South Korea, Taiwan, Hong Kong, Singapore*

These East Asian economies share Confucian-influenced values often linked with sustained economic growth.

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 60 | High power distance; acceptance of authority and hierarchy |
| IDV | 32 | Strong collectivism; family loyalty, group harmony, and collective responsibility |
| MAS | 60 | High masculinity; strong work ethic, ambition, and competition |
| UAI | 58 | Moderate to high uncertainty avoidance; preference for structure and predictability |
| LTO | 80 | Very high long-term orientation; perseverance, thrift, and future focus |
| IVR | 35 | Restrained societies; discipline, self-control, and moderation |

**Key Insight**: Five Dragons cultures balance high collective loyalty with strong ambition and future orientation. Communication should be formal and respectful of hierarchy, frame outcomes in terms of long-term value and group benefit, and maintain a measured, disciplined tone. Avoid casual language or pressure for immediate decisions.

---

### Latin American Cluster
*Mexico, Brazil, Argentina, Chile, Colombia, Peru, Venezuela*

Latin American countries share cultural patterns influenced by colonial history, indigenous traditions, family networks, and social hierarchy.

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 65 | High power distance; acceptance of authority and hierarchical structures |
| IDV | 27 | Strong collectivism; family loyalty and community ties are paramount |
| MAS | 55 | Moderate masculinity; mixed emphasis on achievement and relationships |
| UAI | 82 | High uncertainty avoidance; strong need for rules and predictable outcomes |
| LTO | 22 | Short-term orientation; focus on tradition and social obligations |
| IVR | 62 | Moderate to high indulgence; emphasis on enjoyment and life satisfaction |

**Key Insight**: Latin American cultures combine high power distance and collectivism with strong uncertainty avoidance — hierarchical societies with close family ties and respect for tradition. Acknowledge authority and the relationship before getting to the substance. Provide clear, structured information to reduce anxiety about uncertainty, and close warmly.

---

### Eastern European Cluster
*Russia, Poland, Hungary, Czech Republic, Romania, Bulgaria*

Eastern European countries share historical experiences that appear in their cultural profiles and institutional expectations.

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 65 | High power distance; acceptance of centralised authority |
| IDV | 40 | Moderate collectivism; group loyalty and social ties remain strong |
| MAS | 55 | Moderate masculinity; mixed values on competition and cooperation |
| UAI | 82 | High uncertainty avoidance; strong need for structure and rules |
| LTO | 55 | Moderate to high long-term orientation; pragmatic and adaptable |
| IVR | 25 | Strong restraint; disciplined approach with strict social norms |

**Key Insight**: Eastern European countries combine high power distance, high uncertainty avoidance, and restraint — a cautious approach to change with strong institutional structures. Use a formal, structured tone. Provide detailed, rule-based reasoning. Avoid casual language and emotional appeals; favour logic, precedent, and procedural clarity.

---

## Activation

Activate when the user includes **"context-adapter"** anywhere in their message.

After "context-adapter", the user may provide input in one of three formats:

| Format | Example | What to extract |
|---|---|---|
| Trigger + country + text | `context-adapter Brazil explain how to reset a password` | COUNTRY = Brazil, CONTENT_TO_ADAPT = the remaining text |
| Trigger + text (no country) | `context-adapter explain how to reset a password` | No country detected, CONTENT_TO_ADAPT = all text after trigger |
| Trigger only | `context-adapter` | No country, no content |

**Detecting whether a country was provided**: Check if the first word (or first two words for multi-word country names) after "context-adapter" matches a country name or adjective in the Country Dimensions Table (e.g., "Brazil", "Brazilian", "Germany", "German", "Japan", "Japanese"). If it matches, treat it as the COUNTRY and everything after it as CONTENT_TO_ADAPT. If it does not match a known country, treat the entire text after "context-adapter" as CONTENT_TO_ADAPT.

**If no content was provided** (trigger only, or trigger + country only), ask: "What text would you like me to adapt?"

---

## Step 1 — Ask for the target culture (if not already provided)

**If a country was already identified in the prompt**, skip this step entirely and proceed directly to Step 2.

**If no country was provided**, ask the user:

> "What is the nationality of your target customer? (e.g., Brazilian, German, Japanese)
> Or, if you prefer, you can simply say **High-Context** or **Low-Context** directly."

Wait for the user's response before continuing.

---

## Step 2 — Determine context level and read dimensions

**Look up the country** in the Country Dimensions Table at the bottom of this skill. Read all available values: PDI, IDV, MAS, UAI, LTO, IVR, and Context Score.

- Context score **≥ 50** → **High-Context**
- Context score **< 50** → **Low-Context**
- Context score **blank or Ask user** → Derive the level from the dimension profile: if PDI and/or IDV point clearly to one direction, use that; otherwise ask the user.
- Country **not in the table** → Ask: "I don't have data for that nationality. Would you prefer High-Context or Low-Context style?"

Store dimension values as **PDI, IDV, MAS, UAI, LTO, IVR**. Any value shown as **?** is uncertain — do not apply that dimension's nuance.

Also check whether the country belongs to one of the five Regional Cultural Clusters above. If it does, note the cluster's Key Insight and carry it into Step 3 as additional context.

**If the user said "High-Context", "High", "Low-Context", or "Low"** instead of a country name, use that directly. No dimension or cluster data will be available — apply base style only.

→ **Result: CONTEXT_LEVEL** + dimension values where available + cluster insight if applicable

---

## Step 3 — Adapt the content

Rewrite CONTENT_TO_ADAPT as a full, polished customer-facing response.

**First**, apply the base style rules for the CONTEXT_LEVEL:

### High-Context Base Style

- **Open** with a warm, relationship-building sentence that acknowledges the customer
- **Build context before the main point** — explain the "why" before the "how"
- **Use at least one analogy, metaphor, or real-world example** to illustrate the key concept
- **Use flowing prose** over bullet lists — connect ideas with transitions
- **Respect hierarchy and face** — frame issues as shared challenges, not individual failures
- **Close** with an open, collaborative invitation (e.g., "Please do not hesitate to reach out should you have any further questions")
- **Tone**: warm, patient, contextual, personal
- **Avoid**: cold or blunt phrasing, transactional language that ignores the relationship

### Low-Context Base Style

- **Lead immediately with the key point** — no preamble before the substance
- **Use short, factual sentences**
- **Use bullet points or numbered steps** when listing actions or multiple items
- **State all expectations explicitly** — leave nothing implied or assumed
- **Avoid analogies or extended context** unless strictly necessary for clarity
- **Close** with a clear, specific next step or call to action
- **Tone**: professional, direct, efficient
- **Avoid**: vague wording, implied expectations, and unstated assumptions

**Then**, layer in dimension nuances (skip any dimension marked ?):

- **PDI > 60**: Formal salutation; acknowledge seniority; avoid direct challenge or criticism
- **PDI < 40**: Egalitarian tone; first names acceptable; non-hierarchical language
- **IDV < 40**: "We" framing; group benefit and harmony over individual outcome
- **IDV > 60**: "You" framing; personal benefit and individual empowerment
- **MAS > 60**: Results-focused and assertive; lead with outcomes
- **MAS < 40**: Collaborative; emphasise shared success and mutual care
- **UAI > 70**: Step-by-step structure; eliminate all ambiguity; state every assumption explicitly
- **UAI < 40**: Concise and flexible; no need for exhaustive detail
- **LTO > 60**: Emphasise long-term reliability, continuity, and future benefits
- **LTO < 30**: Emphasise immediate resolution and concrete near-term outcomes
- **IVR > 60**: Warmer and more expressive tone; positive, upbeat closing
- **IVR < 35**: Measured and formal tone; restrained emotional expression

While adapting, note which dimensions triggered a rule — you will need them for the preface.

**Finally**, if the country belongs to a Regional Cultural Cluster, apply the cluster's Key Insight as a final layer of nuance.

---

## Output Format

Present the response in the following fixed order. Do **not** deviate from this structure.

---

### 1. Preface

For each dimension, generate a 10-block visual scale using these rules:

- Scale: 0–120, each block = 12 points
- Filled blocks: `min(round(score / 12), 10)`
- Colour: score < 48 → 🟦 | score 48–72 → 🟨 | score > 72 → 🟧
- Empty blocks: ⬜
- Unknown (?): ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜

**Header line rule**: If the country belongs to a Regional Cultural Cluster, write `[Country] | Cluster: [cluster name]`. If there is no cluster match, write only `[Country]` — omit the "| Cluster:" part entirely.

Header line, then one entry per dimension (scale bar on the same line as the metric, insight on the next line with a blank line between them), then the context score line:

```
[Country] | Cluster: [cluster name]

**Power Distance: [PDI value]** [scale bar]

[driver note if rule triggered, or general definition if not]

**Individualism: [IDV value]** [scale bar]

[driver note if rule triggered, or general definition if not]

**Masculinity: [MAS value]** [scale bar]

[driver note if rule triggered, or general definition if not]

**Uncertainty Avoidance: [UAI value]** [scale bar]

[driver note if rule triggered, or general definition if not]

**Long-Term Orientation: [LTO value]** [scale bar]

[driver note if rule triggered, or general definition if not]

**Indulgence: [IVR value]** [scale bar]

[driver note if rule triggered, or general definition if not]

**Context Score: [score] → [High/Low]-Context**
```

**Rules for each dimension line:**
- If the dimension **triggered a writing rule** (exceeded a threshold): write a short plain-language description of what was specifically applied to the text
- If the dimension **did not trigger a rule**: write the short general definition from the neutral-range entries below:
  - PDI neutral: *Measures acceptance of hierarchy and unequal distribution of power in society*
  - IDV neutral: *Measures the degree to which individuals act independently vs. as part of a group*
  - MAS neutral: *Measures the distribution between assertive, competitive values and nurturing, collaborative values in society*
  - UAI neutral: *Measures tolerance for ambiguity and the need for rules and predictable structure*
  - LTO neutral: *Measures whether a society values future rewards or present and tradition-based priorities*
  - IVR neutral: *Measures the degree to which societies allow free gratification of desires vs. regulation through strict norms*
- Show **?** for any uncertain value and use the neutral definition
- If the user chose High/Low directly (no country): replace the preface with a single line: `Context level: [High/Low] | Source: user preference` and skip the dimension lines

---

### 2. Disclaimer

> **Please note** that this skill is focused on providing suggestions on how to adapt language to certain cultures, however should not be used as an objective guidance on how to communicate with any given person. Despite certain locations tending towards a certain level of context in their communication, individualism still needs to be considered and the language used with customers should always be adapted to each situation and person.
>
>
> More information on the context rating and metrics can be found on the following link: [High and Low-Context Cultures](https://classwrites.com/high-and-low-context-cultures-countries)

---

### 3. Adapted Response

The full rewritten text. No metadata footer after it.

---

**Example output (Hungary):**

Hungary | Cluster: Eastern European

**Power Distance: 46** 🟦🟦🟦🟦⬜⬜⬜⬜⬜⬜

Measures acceptance of hierarchy and unequal distribution of power in society

**Individualism: 80** 🟧🟧🟧🟧🟧🟧🟧⬜⬜⬜

"you" framing, direct personal address

**Masculinity: 88** 🟧🟧🟧🟧🟧🟧🟧⬜⬜⬜

lead with outcomes, assertive tone

**Uncertainty Avoidance: 82** 🟧🟧🟧🟧🟧🟧🟧⬜⬜⬜

step-by-step structure, zero ambiguity

**Long-Term Orientation: 58** 🟨🟨🟨🟨🟨⬜⬜⬜⬜⬜

Measures whether a society values future rewards or present and tradition-based priorities

**Indulgence: 31** 🟦🟦🟦⬜⬜⬜⬜⬜⬜⬜

measured, formal tone; no warmth filler

**Context Score: 27.8 → Low-Context**

---

## Country Dimensions Table

Context score **≥ 50** = High-Context. **< 50** = Low-Context. **?** = uncertain data.

| CTR | Country | PDI | IDV | MAS | UAI | LTO | IVR | Ctx Score | Level |
|---|---|---|---|---|---|---|---|---|---|
| AFE | Africa East | 64 | 27 | 41 | 52 | 32 | 40 | 70.3 | High |
| AFW | Africa West | 77 | 20 | 46 | 54 | 9 | 78 | 79.1 | High |
| ALB | Albania | ? | ? | ? | ? | 61 | 15 | 70.0 | High |
| ALG | Algeria | ? | ? | ? | ? | 26 | 32 | 67.4 | High |
| AND | Andorra | ? | ? | ? | ? | ? | 65 | ? | Ask user |
| ARA | Arab countries | 80 | 38 | 53 | 68 | 23 | 34 | 67.4 | High |
| ARG | Argentina | 49 | 46 | 56 | 86 | 20 | 62 | 52.5 | High |
| ARM | Armenia | ? | ? | ? | ? | 61 | ? | 70.0 | High |
| AUL | Australia | 38 | 90 | 61 | 51 | 21 | 71 | 18.4 | Low |
| AUT | Austria | 11 | 55 | 79 | 70 | 60 | 63 | 34.8 | Low |
| AZE | Azerbaijan | ? | ? | ? | ? | 61 | 22 | 70.0 | High |
| BAN | Bangladesh | 80 | 20 | 55 | 60 | 47 | 20 | 80.0 | High |
| BLR | Belarus | ? | ? | ? | ? | 81 | 15 | 70.0 | High |
| BEL | Belgium | 65 | 75 | 54 | 94 | 82 | 57 | 37.0 | Low |
| BEF | Belgium French | 67 | 72 | 60 | 93 | ? | ? | 39.7 | Low |
| BEN | Belgium Netherl | 61 | 78 | 43 | 97 | ? | ? | 33.7 | Low |
| BOS | Bosnia | ? | ? | ? | ? | 70 | 44 | 70.0 | High |
| BRA | Brazil | 69 | 38 | 49 | 76 | 44 | 59 | 64.1 | High |
| BUL | Bulgaria | 70 | 30 | 40 | 85 | 69 | 16 | 70.0 | High |
| BUF | Burkina Faso | ? | ? | ? | ? | 27 | 18 | 79.1 | High |
| CAN | Canada | 39 | 80 | 52 | 48 | 36 | 68 | 25.7 | Low |
| CAF | Canada French | 54 | 73 | 45 | 60 | ? | ? | 35.1 | Low |
| CHL | Chile | 63 | 23 | 28 | 86 | 31 | 68 | 72.8 | High |
| CHI | China | 80 | 20 | 66 | 30 | 87 | 24 | 80.0 | High |
| COL | Colombia | 67 | 13 | 64 | 80 | 13 | 83 | 81.0 | High |
| COS | Costa Rica | 35 | 15 | 21 | 86 | ? | ? | 70.0 | High |
| CRO | Croatia | 73 | 33 | 40 | 80 | 58 | 33 | 68.8 | High |
| CYP | Cyprus | ? | ? | ? | ? | ? | 70 | 57.5 | High |
| CZE | Czech Rep | 57 | 58 | 57 | 74 | 70 | 29 | 46.5 | Low |
| DEN | Denmark | 18 | 74 | 16 | 23 | 35 | 70 | 23.6 | Low |
| DOM | Dominican Rep | ? | ? | ? | ? | 13 | 54 | 68.5 | High |
| ECA | Ecuador | 78 | 8 | 63 | 67 | ? | ? | 87.8 | High |
| EGY | Egypt | ? | ? | ? | ? | 7 | 4 | 67.4 | High |
| ETH | Ethiopia | ? | ? | ? | ? | ? | 46 | 70.3 | High |
| SAL | El Salvador | 66 | 19 | 40 | 94 | 20 | 89 | 76.5 | High |
| EST | Estonia | 40 | 60 | 30 | 60 | 82 | 16 | 40.0 | Low |
| FIN | Finland | 33 | 63 | 26 | 59 | 38 | 57 | 35.8 | Low |
| FRA | France | 68 | 71 | 43 | 86 | 63 | 48 | 40.7 | Low |
| GEO | Georgia | ? | ? | ? | ? | 38 | 32 | 70.0 | High |
| GER | Germany | 35 | 67 | 66 | 65 | 83 | 40 | 33.6 | Low |
| GEE | Germany East | ? | ? | ? | ? | 78 | 34 | 33.6 | Low |
| GHA | Ghana | ? | ? | ? | ? | 4 | 72 | 79.1 | High |
| GBR | Great Britain | 35 | 89 | 66 | 35 | 51 | 69 | 18.2 | Low |
| GRE | Greece | 60 | 35 | 57 | 112 | 45 | 50 | 63.5 | High |
| GUA | Guatemala | 95 | 6 | 37 | 101 | ? | ? | 94.3 | High |
| HOK | Hong Kong | 68 | 25 | 57 | 29 | 61 | 17 | 72.9 | High |
| HUN | Hungary | 46 | 80 | 88 | 82 | 58 | 31 | 27.8 | Low |
| ICE | Iceland | ? | ? | ? | ? | 28 | 67 | 54.5 | High |
| IND | India | 77 | 48 | 56 | 40 | 51 | 26 | 59.5 | High |
| IDO | Indonesia | 78 | 14 | 46 | 48 | 62 | 38 | 83.6 | High |
| IRA | Iran | 58 | 41 | 43 | 59 | 14 | 40 | 58.7 | High |
| IRQ | Iraq | ? | ? | ? | ? | 25 | 17 | 67.4 | High |
| IRE | Ireland | 28 | 70 | 68 | 35 | 24 | 65 | 29.4 | Low |
| ISR | Israel | 13 | 54 | 47 | 81 | 38 | ? | 36.1 | Low |
| ITA | Italy | 50 | 76 | 70 | 75 | 61 | 30 | 31.8 | Low |
| JAM | Jamaica | 45 | 39 | 68 | 13 | ? | ? | 56.2 | High |
| JPN | Japan | 54 | 46 | 95 | 92 | 88 | 42 | 54.0 | High |
| JOR | Jordan | ? | ? | ? | ? | 16 | 43 | 67.4 | High |
| KOR | Korea South | 60 | 18 | 39 | 85 | 100 | 29 | 75.4 | High |
| KYR | Kyrgyz Rep | ? | ? | ? | ? | 66 | 39 | 70.0 | High |
| LAT | Latvia | 44 | 70 | 9 | 63 | 69 | 13 | 34.2 | Low |
| LIT | Lithuania | 42 | 60 | 19 | 65 | 82 | 16 | 40.6 | Low |
| LUX | Luxembourg | 40 | 60 | 50 | 70 | 64 | 56 | 40.0 | Low |
| MAC | Macedonia Rep | ? | ? | ? | ? | 62 | 35 | 70.0 | High |
| MAL | Malaysia | 104 | 26 | 50 | 36 | 41 | 57 | 83.0 | High |
| MLI | Mali | ? | ? | ? | ? | 20 | 43 | 79.1 | High |
| MLT | Malta | 56 | 59 | 47 | 96 | 47 | 66 | 45.5 | Low |
| MEX | Mexico | 81 | 30 | 69 | 82 | 24 | 97 | 73.3 | High |
| MOL | Moldova | ? | ? | ? | ? | 71 | 19 | 70.0 | High |
| MNG | Montenegro | ? | ? | ? | ? | 75 | 20 | 70.0 | High |
| MOR | Morocco | 70 | 46 | 53 | 68 | 14 | 25 | 58.8 | High |
| NET | Netherlands | 38 | 80 | 14 | 53 | 67 | 68 | 25.4 | Low |
| NZL | New Zealand | 22 | 79 | 58 | 49 | 33 | 75 | 21.3 | Low |
| NIG | Nigeria | ? | ? | ? | ? | 13 | 84 | 79.1 | High |
| NOR | Norway | 31 | 69 | 8 | 50 | 35 | 55 | 31.0 | Low |
| PAK | Pakistan | 55 | 14 | 50 | 70 | 50 | 0 | 76.7 | High |
| PAN | Panama | 95 | 11 | 44 | 86 | ? | ? | 90.8 | High |
| PER | Peru | 64 | 16 | 42 | 87 | 25 | 46 | 78.0 | High |
| PHI | Philippines | 94 | 32 | 64 | 44 | 27 | 42 | 75.8 | High |
| POL | Poland | 68 | 60 | 64 | 93 | 38 | 29 | 48.4 | Low |
| POR | Portugal | 63 | 27 | 31 | 104 | 28 | 33 | 70.0 | High |
| PUE | Puerto Rico | ? | ? | ? | ? | 0 | 90 | ? | Ask user |
| ROM | Romania | 90 | 30 | 42 | 90 | 52 | 20 | 76.0 | High |
| RUS | Russia | 93 | 39 | 36 | 95 | 81 | 20 | 70.6 | High |
| RWA | Rwanda | ? | ? | ? | ? | 18 | 37 | 70.3 | High |
| SAU | Saudi Arabia | ? | ? | ? | ? | 36 | 52 | 67.4 | High |
| SER | Serbia | 86 | 25 | 43 | 92 | 52 | 28 | 78.3 | High |
| SIN | Singapore | 74 | 20 | 48 | 8 | 72 | 46 | 78.2 | High |
| SLK | Slovak Rep | 104 | 52 | 110 | 51 | 77 | 28 | 64.8 | High |
| SLV | Slovenia | 71 | 27 | 19 | 88 | 49 | 48 | 72.4 | High |
| SAF | South Africa | ? | ? | ? | ? | 34 | 63 | 39.2 | Low |
| SAW | South Africa white | 49 | 65 | 63 | 49 | ? | ? | 39.2 | Low |
| SPA | Spain | 57 | 51 | 42 | 86 | 48 | 44 | 51.4 | High |
| SUR | Suriname | 85 | 47 | 37 | 92 | ? | ? | 62.6 | High |
| SWE | Sweden | 31 | 71 | 5 | 29 | 53 | 78 | 29.6 | Low |
| SWI | Switzerland | 34 | 68 | 70 | 58 | 74 | 66 | 32.6 | Low |
| SWF | Switzerland French | 70 | 64 | 58 | 70 | ? | ? | 46.2 | Low |
| SWG | Switzerland German | 26 | 69 | 72 | 56 | ? | ? | 29.5 | Low |
| TAI | Taiwan | 58 | 17 | 45 | 69 | 93 | 49 | 75.5 | High |
| TAN | Tanzania | ? | ? | ? | ? | 34 | 38 | 70.3 | High |
| THA | Thailand | 64 | 20 | 34 | 64 | 32 | 45 | 75.2 | High |
| TRI | Trinidad and Tobago | 47 | 16 | 58 | 55 | 13 | 80 | 72.9 | High |
| TUR | Turkey | 66 | 37 | 45 | 85 | 46 | 49 | 63.9 | High |
| USA | U.S.A. | 40 | 91 | 62 | 46 | 26 | 68 | 18.3 | Low |
| UGA | Uganda | ? | ? | ? | ? | 24 | 52 | 70.3 | High |
| UKR | Ukraine | ? | ? | ? | ? | 86 | 14 | 70.0 | High |
| UZB | Uzbekistan | 70 | 40 | 50 | 60 | 50 | 35 | 63.0 | High |
| URU | Uruguay | 61 | 36 | 38 | 100 | 26 | 53 | 63.1 | High |
| VEN | Venezuela | 81 | 12 | 73 | 76 | 16 | 100 | 85.9 | High |
| VIE | Vietnam | 70 | 20 | 40 | 30 | 57 | 35 | 77.0 | High |
| ZAM | Zambia | ? | ? | ? | ? | 30 | 42 | 79.1 | High |
| ZIM | Zimbabwe | ? | ? | ? | ? | 15 | 28 | 79.1 | High |