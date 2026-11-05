---
name: culture-call-advisor
description: >-
  Provides cultural communication guidance for a business call based on the target person's country and Hofstede dimensions. Activate when the user includes "context-advisor" in their message. Given a call topic and a country (or a High/Low-Context preference), it produces a cultural preface with Hofstede dimension metrics, a general call briefing covering tone, assertiveness, hierarchy, and pacing, and specific call insights tailored to the topic (question style, side conversations, personal references, opening/closing, objection handling). Trigger phrases include: "context-advisor", "/context-advisor", "context advisor".
metadata:
  author: Leonardo Felini
  version: 1.2.0
  tags: communication culture calls hofstede high-context low-context sales customer
---


# Culture Call Advisor

This skill provides cultural communication guidance for a business call. Given a call topic and a target person's country (or a direct High/Low-Context preference), it produces a cultural preface, a general call briefing, and topic-specific insights to help the user communicate effectively.

---

## Activation

Activate when the user includes **"context-advisor"** anywhere in their message.

After "context-advisor", the user may provide input in one of these formats:

| Format | Example | What to extract |
|---|---|---|
| Trigger + country + topic | `context-advisor Brazil product upsell` | COUNTRY = Brazil, TOPIC = product upsell |
| Trigger + country | `context-advisor Brazil` | COUNTRY = Brazil, TOPIC = none |
| Trigger only | `context-advisor` | No country, no topic |

**Detecting a country**: Check if the first word (or first two words for multi-word names) after "context-advisor" matches a country name or adjective in the Country Dimensions Table (e.g. "Brazil", "Brazilian", "Germany", "German"). If it matches, treat it as COUNTRY and everything after as TOPIC. If it matches "high", "high-context", "low", or "low-context", treat it as a direct context level preference (see Step 1). If neither, treat the entire text after "context-advisor" as TOPIC with no country.

---

## Step 1 — Gather missing inputs

### Country
**If a country or context level was already identified**, skip to Step 2.

**If no country was provided**, ask:

> "Which country is the person you're calling from?
> You can also simply say **High-Context** or **Low-Context** if you prefer a more general approach — though specific country data will give you more precise guidance."

Wait for the user's response before continuing.

### Topic
**If a topic was already identified**, skip this step.

**If no topic was provided**, ask:

> "Do you have a specific topic for this call? Sharing it helps me tailor the insights — but if you'd prefer general guidance, just say so."

Wait for the user's response before continuing.

---

## Step 2 — Determine context level and load dimensions

**If a country name was provided**: Look it up in the Country Dimensions Table. Read all values: PDI, IDV, MAS, UAI, LTO, IVR, and Context Score.

- Context score **≥ 50** → **High-Context**
- Context score **< 50** → **Low-Context**
- Context score **blank or "Ask user"** → Derive from PDI and IDV direction; if still unclear, ask the user
- Country **not in the table** → Ask: "I don't have specific data for that country. Would you prefer **High-Context** or **Low-Context** style?"

Also check whether the country belongs to one of the five Regional Cultural Clusters below. If it does, note the cluster's Key Insight — apply it when writing the briefing and insights.

Set **GENERIC_MODE = false**.

**If the user said "High-Context", "High", "Low-Context", or "Low"**: No dimension data is available. Set CONTEXT_LEVEL accordingly. Set **GENERIC_MODE = true**.

---

## Step 3 — Generate output

Present the response in the following fixed order. Do **not** deviate from this structure.

---

### Section 1: Preface

**If GENERIC_MODE = false (country-based)**:

For each dimension, generate a 10-block visual scale using these rules:

- Scale: 0–120, each block = 12 points
- Filled blocks: `min(round(score / 12), 10)`
- Colour: score < 48 → 🟦 | score 48–72 → 🟨 | score > 72 → 🟧
- Empty blocks: ⬜
- Unknown (?): show ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜

Format each dimension line as follows — the scale bar and description are on separate lines with a blank line between them:

```
[Country] | Cluster: [cluster name, or "No regional cluster match"]

**Power Distance: [PDI]** [scale bar]

Measures acceptance of hierarchy and unequal distribution of power in society

**Individualism: [IDV]** [scale bar]

Measures the degree to which individuals act independently vs. as part of a group

**Masculinity: [MAS]** [scale bar]

Measures the distribution between assertive, competitive values and nurturing, collaborative values in society

**Uncertainty Avoidance: [UAI]** [scale bar]

Measures tolerance for ambiguity and the need for rules and predictable structure

**Long-Term Orientation: [LTO]** [scale bar]

Measures whether a society values future rewards or present and tradition-based priorities

**Indulgence: [IVR]** [scale bar]

Measures the degree to which societies allow free gratification of desires vs. regulation through norms

**Context Score: [score] → [High/Low]-Context**
```

For uncertain values (**?**): show the score as `?` and the scale bar as ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜.

**If GENERIC_MODE = true (user said High/Low directly)**:

```
Context level: [High/Low]-Context | Source: user preference

> ⚠ This guidance was generated using generic [High/Low]-Context characteristics, without specific country data. Insights may be less precise than country-specific guidance.
```

---

### Section 2: Disclaimer

> **Please note** that this skill is intended to provide guidance on how to approach a business call with someone from a certain cultural background, and should not be used as an objective rulebook for communicating with any given person. Despite certain locations tending towards a certain level of context in their communication, individual variation always applies — adapt your approach to each situation and person.
>
> More information on the context rating and metrics can be found here: [High and Low-Context Cultures](https://classwrites.com/high-and-low-context-cultures-countries)

---

### Section 3: General Call Briefing

Write 3–5 bullet points advising how to approach the call in general. Cover:

- **Tone**: formal vs. informal, warm vs. transactional
- **Assertiveness**: direct vs. indirect communication style
- **Pacing**: fast-paced and action-oriented vs. deliberate and relationship-building
- **Hierarchy**: whether to acknowledge seniority or communicate as peers
- **Relationship vs. Task orientation**: how much time to invest in rapport before getting to business

Apply these dimension thresholds to derive specific guidance (skip any dimension marked **?**):

- PDI > 60: acknowledge hierarchy and seniority; formal tone; avoid direct pushback
- PDI < 40: egalitarian, peer-level communication; first names acceptable
- IDV < 40: frame outcomes in group or team terms; relationship and harmony first
- IDV > 60: frame outcomes in personal benefit terms; direct and self-reliant tone
- MAS > 60: results-focused; assertive; lead with outcomes
- MAS < 40: collaborative; emphasise shared benefit and mutual care
- UAI > 70: structured and detailed; provide a clear agenda upfront; eliminate ambiguity
- UAI < 40: flexible; no need for rigid structure or exhaustive detail
- LTO > 60: frame the call in terms of long-term relationship and future value
- LTO < 30: focus on immediate outcomes and near-term resolution
- IVR > 60: warmer and more expressive opening is welcome; upbeat tone
- IVR < 35: measured and formal; avoid casual or overly cheerful phrasing

If the country belongs to a Regional Cultural Cluster, apply its Key Insight as a final layer.

If GENERIC_MODE = true, base guidance only on the general High/Low-Context characteristics (see Cultural Context Framework below), without dimension-specific rules.

---

### Section 4: Call Insights

Provide 4–6 specific, actionable tips for the call. If a TOPIC was provided, tailor each tip to it. If no topic was given, provide general communication tips.

Address the most relevant of these angles for the cultural profile and topic:

- **Question style**: Open questions (explore, build rapport, let the other person lead) vs. closed questions (confirm, control the flow, drive to a decision). High-context cultures generally respond better to open questions; low-context cultures often appreciate direct, closed questions for efficiency. That said, open questions remain a strong choice in any cultural context when you are unsure what you are looking for, or when you want the other person to elaborate more thoroughly — use them intentionally regardless of context level.
- **Side conversations**: Embrace tangents and personal detours as relationship-building, or gently redirect to stay on-topic. High-context cultures often use side conversations to build trust; low-context cultures may see them as inefficient.
- **Personal references**: Whether mentioning personal topics (family, local events, shared experiences) is advisable, neutral, or likely to feel intrusive. Collectivist cultures generally welcome personal warmth; highly individualist cultures may prefer to keep it professional.
- **Call opening**: Open with small talk and relationship-building, or directly with the agenda.
- **Call closing**: Close with a clear next step and action items, or a warm sign-off that leaves room for follow-up.
- **Objection handling**: Address disagreement directly and factually, or soften it and preserve face.
- **Topic-specific guidance** (only if a TOPIC was provided): Apply the above angles to the specific call topic. For example — if the topic is "upselling", advise on how to frame the pitch; if it is "delivering bad news", advise on how to soften and frame it appropriately; if it is "negotiation", advise on pace, concession style, and decision-making dynamics.

---

## Cultural Context Framework

### High-Context Cultures

- Indirect, nuanced, and relationship-first communication
- Strong emphasis on saving face and preserving harmony
- Non-verbal cues, silence, and timing carry real meaning
- Trust in relationships matters more than written contracts
- Meaning lives in situation, relationship, and shared history
- Status and seniority shape who speaks and who decides

### Low-Context Cultures

- Direct, precise, and text-focused communication
- Agreements and expectations are written down
- Conflict is handled openly and quickly
- Meaning is carried mainly by words and documents
- Anyone may speak; ideas are judged on their own merit
- Contracts and procedures replace reliance on relationships

---

## Regional Cultural Clusters

### The Nordic Cluster
*Denmark, Finland, Sweden, Norway, Iceland*

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 19 | Exceptionally low power distance; citizens expect equality and participative decision-making |
| IDV | 69 | Strong individualism; personal responsibility and self-reliance |
| MAS | 25 | Strong femininity; focus on quality of life, cooperation, and gender equality |
| UAI | 40 | Low uncertainty avoidance; tolerant of ambiguity; pragmatic approach |
| LTO | 45 | Moderate long-term orientation; balanced focus on tradition and future |
| IVR | 60 | High indulgence; emphasis on happiness, leisure, and life satisfaction |

**Key Insight**: Communicate as a peer, not an authority. Avoid hierarchy signals and emphasise shared benefit and openness.

---

### The Anglo Cluster
*United States, Canada, Australia, New Zealand, Great Britain, Ireland*

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 38 | Low power distance; people question authority and expect equal rights |
| IDV | 83 | Very high individualism; emphasis on personal freedom, self-reliance, and individual rights |
| MAS | 58 | High masculinity; focus on competition, achievement, and material success |
| UAI | 42 | Low uncertainty avoidance; tolerance for ambiguity and risk-taking |
| LTO | 29 | Short-term orientation; focus on tradition, quick results, and social obligations |
| IVR | 67 | High indulgence; emphasis on enjoying life, freedom of choice, and personal happiness |

**Key Insight**: Lead with the outcome and frame it around what the individual gains.

---

### The Five Dragons
*Japan, South Korea, Taiwan, Hong Kong, Singapore*

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 60 | High power distance; acceptance of authority and hierarchy |
| IDV | 32 | Strong collectivism; family loyalty, group harmony, and collective responsibility |
| MAS | 60 | High masculinity; strong work ethic, ambition, and competition |
| UAI | 58 | Moderate to high uncertainty avoidance; preference for structure and predictability |
| LTO | 80 | Very high long-term orientation; perseverance, thrift, and future focus |
| IVR | 35 | Restrained societies; discipline, self-control, and moderation |

**Key Insight**: Frame outcomes in terms of long-term value and group benefit. Maintain a formal and respectful tone. Avoid casual language or pressure for immediate decisions.

---

### Latin American Cluster
*Mexico, Brazil, Argentina, Chile, Colombia, Peru, Venezuela*

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 65 | High power distance; acceptance of authority and hierarchical structures |
| IDV | 27 | Strong collectivism; family loyalty and community ties are paramount |
| MAS | 55 | Moderate masculinity; mixed emphasis on achievement and relationships |
| UAI | 82 | High uncertainty avoidance; strong need for rules and predictable outcomes |
| LTO | 22 | Short-term orientation; focus on tradition and social obligations |
| IVR | 62 | Moderate to high indulgence; emphasis on enjoyment and life satisfaction |

**Key Insight**: Acknowledge authority and the relationship before getting to the substance. Provide clear, structured information and close warmly.

---

### Eastern European Cluster
*Russia, Poland, Hungary, Czech Republic, Romania, Bulgaria*

| Dimension | Avg. Score | What This Means |
|---|---|---|
| PDI | 65 | High power distance; acceptance of centralised authority |
| IDV | 40 | Moderate collectivism; group loyalty and social ties remain strong |
| MAS | 55 | Moderate masculinity; mixed values on competition and cooperation |
| UAI | 82 | High uncertainty avoidance; strong need for structure and rules |
| LTO | 55 | Moderate to high long-term orientation; pragmatic and adaptable |
| IVR | 25 | Strong restraint; disciplined approach with strict social norms |

**Key Insight**: Use a formal, structured tone. Provide detailed, rule-based reasoning. Avoid casual language and emotional appeals; favour logic, precedent, and procedural clarity.

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
