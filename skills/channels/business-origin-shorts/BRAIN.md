# Channel Brain — Business Origin Shorts ("How X Was Founded")

> The single source of truth for producing this channel's Shorts. Read this file
> top to bottom before touching a pipeline. It tells you **what the video is**,
> **why it works**, **which skills to load**, **which tools to call**, and **how to
> check the result**. Everything here was reverse-engineered from the three
> most-viewed Shorts of the reference channel @PureBusinesshorts (analysed
> beat-by-beat with vidIQ, October 2026).

Style playbook: [`styles/meme-collage-business.yaml`](../../../styles/meme-collage-business.yaml)

---

## 0. Routing — when this brain applies

Load this brain when the user asks for any of:
- "How <brand> was founded", "the story of <company>", "make a PureBusiness-style short"
- a business / brand origin story as a vertical Short
- "a video in the channel style", "next episode", "do <brand> next"

Then follow AGENT_GUIDE Rule Zero as normal: the pipeline is **`animated-explainer`**
(`pipeline_defs/animated-explainer.yaml`, narration + generated images + music), with the
stage directors in `skills/pipelines/explainer/`. Pass `style: meme-collage-business` as the
playbook. This brain overrides creative defaults (pacing,
look, script shape, camera, sound) but never the governance rules (preflight,
decision log, approvals, cost announcements, both-runtime presentation).

---

## 1. The format in one paragraph

A ~45–60 s vertical (1080×1920) narrated history of how a famous brand started.
Real photographic backgrounds of the era and place, crude **red stick-figure
bodies** wearing **real cut-out faces** of the founders (or rage-comic/meme faces
for side characters), hard cuts every 1.5–2.5 s, a **year slammed on screen** to
open each chapter, word-synced bold captions, a sound effect on nearly every
noun, animated money/sales counters, and a one-line **punchline ending** built
around a huge number or an ironic twist.

---

## 2. Reference teardown (what actually went viral)

| # | Video | Views | Length | Hook (first 2 s) | Payoff line |
|---|---|---|---|---|---|
| 1 | How Gillette Was Founded | 8.0 M | 0:57 | "In 1895…" + dull razor (relatable pain) | "P&G bought Gillette for $57 billion." |
| 2 | How Casio Was Founded | 4.7 M | 0:44 | "1946" over Tokyo ruins (underdog) | "It survived everything. It still does." |
| 3 | How Liquid Death Was Founded | 4.0 M | 0:57 | Monster cans secretly hold water (secret) | "Valued at $1.4 billion. It is technically just water." |

Shared patterns, all three:
1. **Year-first open.** Frame 0 is a big year ("1895", "1946", "2009") — instant time-travel signal.
2. **Surprising or relatable seed.** A pain (dull blade), an absurd first product (cigarette ring), or a secret (water in Monster cans).
3. **Obstacle beat.** Experts say impossible / no product, no factory, no money.
4. **Breakthrough + multiplier.** WWI army contract, Facebook virality, G-Shock roof test.
5. **Number climb.** Sales or valuation animate upward on a counter or bar chart.
6. **Punchline close.** Short, declarative, re-watchable. No CTA, no "subscribe".

Measured craft numbers:
- **Visual change:** every 0.5–1.0 s (prop pops), **background change:** every 2–3 s.
- **Narration:** 130–160 words for 45–60 s (≈ 2.6–2.9 words/s), zero filler, sentences ≤ 12 words.
- **SFX density:** ~1 sound per spoken noun/action (pop, whoosh, cha-ching, thud, shatter, stamp).
- **Captions:** 1–3 words at a time, synced to the voice, uppercase.

---

## 3. Script rules (write these before any asset)

Template — fill each slot, keep the order:

```
[0] YEAR + SEED      "In <year>, <founder> <did a mundane thing> when <problem/oddity>."
[1] CONTEXT          1–2 lines: who they were / why nobody solved it.
[2] INSIGHT          The idea, in one sentence a 12-year-old gets.
[3] OBSTACLE         "<Experts / banks / everyone> said <impossible>." or "No product. No factory. No money."
[4] SCRAPPY START    First tiny numbers ("sold 51 razors"), garage, trunk of a car.
[5] MULTIPLIER       The event that blew it up (war, athlete, viral ad, regulation).
[6] NUMBER CLIMB     2–3 escalating numbers in a row.
[7] PUNCHLINE        Final valuation / acquisition / ironic truth. ≤ 10 words. Then stop.
```

Rules:
- 130–160 words total. Read it aloud: if it exceeds 60 s at a brisk pace, cut beat [1] first.
- Every sentence must be **visualisable** — if you can't name the prop/background, rewrite it.
- Prefer concrete numbers, dates, names over adjectives.
- Facts must be **verified** (research stage, ≥ 2 sources). Mark any shaky number and soften it ("about", "nearly"). Never invent quotes.
- No intro ("Today we're looking at…"), no outro, no "subscribe". The punchline is the last word.
- Title format: `How <Brand> Was Founded <emoji> #shorts #business`.

---

## 4. Visual system (see the style YAML for exact tokens)

Layer stack, back to front, per scene:
1. **Background plate** — photographic, era- and place-accurate (1960s running track, 1940s Tokyo rubble, 2009 festival stage). Full-bleed 1080×1920, slightly over-scaled (≥ 110 %) so camera moves never reveal edges.
2. **Props** — real-object cutouts with hard edges (a razor, a waffle iron, a cheque, money bags, a patent document). Pop in with overshoot.
3. **Characters** — red (#E3201B) stick-figure bodies, 10–14 px rounded strokes, with a **head = cut-out photo face** of the real person, ~1.6× realistic head scale. Side characters (customers, engineers, bosses) use rage-comic / meme faces. Limbs animate in 2–4-frame stepped poses (stop-motion feel, not smooth tweening).
4. **Data layer** — counters, bar charts, valuation bars, red ❌ / green ✅ badges, "$" stacks.
5. **Year card** — huge white year with black stroke, slammed in at each chapter.
6. **Captions** — see §6.

Asset rules:
- One background per beat of the script (expect 8–12 plates per video).
- Faces: obtain a real reference photo of each founder, then cut out (bg removal) and optionally stylise via image-to-image so it stays recognisable. Recognisability > polish.
- The brand logo/product appears in at least 3 beats (opening seed, launch, punchline).
- Keep everything inside the YouTube Shorts safe zone (984×1500 centred; top 120 px and bottom 300 px stay clear of captions and key faces).

---

## 5. Camera language (fast-cut meme-collage edition)

Every shot gets **exactly one** camera intention. The camera is a wrapper
transform around the whole scene layer (background + characters + props); see
`yt-camera-move` below for the reference implementation.

| Move | When | Parameters |
|---|---|---|
| **Snap zoom / punch-in** | On a key noun or number ("$57 BILLION", "1957") | scale 1.0 → 1.25–1.45 in 0.25–0.35 s, `power3.out`; hold |
| **Slow push-in** | Default for any shot ≥ 2 s with no other move ("the scene is alive") | scale 1.00 → 1.06–1.10 across the whole shot, `sine.inOut` |
| **Whip pan** | Location/time change between scenes | translateX ±110 % over 0.18–0.25 s + 20–40 px horizontal motion blur, `power4.in` out / `power4.out` in |
| **Pan across** | Showing a crowd, a factory floor, a store shelf, a timeline | translateX 8–15 % across the shot, `none` or `sine.inOut` |
| **Tilt down / follow fall** | Something drops (watch off a roof, money rain) | translateY following the object, `power2.in` |
| **Camera shake** | Impact: stamp, crash, rejection, explosion, big reveal | 3–6 hits of ±8–18 px + ±1–2° over 0.15–0.3 s, decaying |
| **Zoom-out reveal** | "It was the size of a desk", "every soldier" — scale reveal | scale 1.6 → 1.0 in 0.45–0.6 s, `power3.inOut` |
| **Push to number** | Final punchline value | 1.0 → 1.8 over 0.55 s, `power3.inOut`, + shake on land |

Craft rules (adapted from huashu-design `camera-language.md` and HyperFrames' camera vocabulary):
- **Zoom duration scales with zoom amount**: `duration = 0.55 × |ln(z2/z1)| / ln 2`, clamped to [0.25, 0.9] s. Fixed durations look amateur.
- **Speed comes from acceleration, not constant speed.** Never linear on a move with a start and an end point; use `power3/power4`. Linear only for constant drift.
- **No pumping**: never zoom out-then-in between two adjacent shots less than 1.5 s apart; carry the current scale into the next move.
- **Pin the hero**: when the background scales, the face/prop the narration names must stay inside the centre 80 % of frame.
- **Move on the beat**: start the move 0.1–0.15 s *before* the word it emphasises, so the camera lands on the word.
- **Over-scan plates** (≥ 110 %) so pans/shakes never expose an edge.
- **Budget**: this genre tolerates far more camera activity than product demos (calm-demo rules like "≥ 2.6 s between moves" do **not** apply), but no more than one *large* move (punch-in, whip, zoom-out) per 1.5 s.

Reference implementations to read:
- `.agents/skills/hyperframes-animation/` — `rules/multi-phase-camera.md`, `rules/coordinate-target-zoom.md`, `rules/motion-blur-streak.md`, `rules/viewport-change.md`, `transitions/`, `blueprints/dataviz-countup.md`, `blueprints/kinetic-type-beats.md`
- HyperFrames registry component **`yt-camera-move`** (Camera Punch-In: zoom, slide, 3D tilt-pan helpers + edge-defocus pulse) — https://github.com/heygen-com/hyperframes/tree/main/registry/components/yt-camera-move. In atelier mode read it as a **mechanics reference**, don't paste it as a look.
- HyperFrames camera vocabulary — https://github.com/heygen-com/hyperframes/blob/main/docs/prompting/vocabulary.mdx
- huashu-design camera language (zoom-duration formula, inter-shot grammar, easing table) — https://github.com/alchaincyf/huashu-design/blob/main/references/camera-language.md

---

## 6. Captions

- Font: heavy condensed sans (Anton / Bebas Neue / Montserrat Black), UPPERCASE, white fill, 6–8 px black stroke, soft drop shadow.
- 1–3 words per card, swapped on the word (word-level timestamps from the TTS or a transcriber).
- Position: upper third (y ≈ 22–30 % of frame) so faces in the middle stay clear and the Shorts UI at the bottom doesn't cover it.
- Pop-in: scale 0.6 → 1.08 → 1.0 in ~0.12 s. Numbers and money get **green (#22C55E)** or **gold (#FACC15)** fill; danger/negatives get **red (#E3201B)**.
- Year cards are separate from captions: 260–340 px, slammed in with a shake.
- Skills: `skills/creative/typography.md`, `.agents/skills/hyperframes-animation/blueprints/kinetic-type-beats.md`, `rules/asr-keyword-glow.md`, `.agents/skills/hyperframes-media` (captions section).

---

## 7. Sound

| Layer | Spec |
|---|---|
| Voice | Confident, slightly fast storyteller (≈ 165–175 wpm), no breaths left in, punchy stops. Loudest layer. |
| Music | Light curious/upbeat lo-fi or plucky corporate groove, 95–115 BPM, -22 to -26 dB under voice, ducked further on the punchline. |
| SFX | One per action/noun: pop (prop in), whoosh (whip pan), cha-ching / coin (money), stamp (deal/contract), thud (fall/impact), glass shatter, buzzer (rejection), notification ding (viral), crowd murmur, page flip (calendar). Short (≤ 0.6 s), placed 0–40 ms before the visual. |
| Final mix | -14 LUFS integrated, true peak ≤ -1 dBTP (see `skills/creative/short-form.md`). |

Skills: `skills/creative/sound-design.md`, `.agents/skills/sound-effects`, `.agents/skills/hyperframes-media`.

---

## 8. Providers for this channel

The channel owner has chosen these providers. Announce them before any paid call (AGENT_GUIDE "Decision Communication Contract").

| Need | Provider | Env var | Notes |
|---|---|---|---|
| Narration (TTS) | **OpenRouter → Fish Audio S2.1 Pro** | `OPENROUTER_API_KEY` | Confirm the exact model slug on openrouter.ai/models before the first call. OpenMontage's native `fish_audio_tts` tool also supports `s2.1-pro` but bills fish.audio directly via `FISH_AUDIO_API_KEY`; use it only if the owner switches billing. |
| Text-to-image (backgrounds, props) | **Kie.ai** (cheapest available T2I model) | `KIE_API_KEY` | Async task API: create a task, then poll for the result URL. Check https://docs.kie.ai for the current endpoints and model names. |
| Image-to-image (face cut-outs, style matching) | **Kie.ai** (I2I / edit model) | `KIE_API_KEY` | Feed a real founder photo → "isolated head, white background, same identity". |
| Composition | HyperFrames (Remotion if installed) | — | Present both if both are available (HARD RULE). |
| Analysis of new references | vidIQ connector (`vidiq_channel_videos`, `vidiq_watch_shortform_content`, `vidiq_video_transcript`) | — | Use to study new top-performing Shorts before a new season. |

**If a tool for OpenRouter TTS or Kie.ai does not yet exist in `tools/`**, follow
`skills/meta/capability-extension.md` to add it as a proper `BaseTool` (`tools/audio/openrouter_tts.py`,
`tools/graphics/kie_image.py`) with a registry entry, cost estimate and `agent_skills` — do **not**
call the APIs from ad-hoc scripts (Rule Zero).

**Network**: in cloud sessions the hosts `openrouter.ai` and `api.kie.ai` (plus Kie's result/CDN host)
must be on the environment's allowed-domains list, and the two keys must be set as environment secrets.

### Image prompt recipes (Kie.ai)

Background plate (T2I):
```
Vertical 9:16 photograph, <place>, <year/era>, <time of day>, realistic documentary
photo, natural light, empty middle ground for characters, no people in the
foreground, no text, no logos, no watermark, sharp, high detail
```
Prop (T2I):
```
Single <object> from <era>, isolated on pure white background, product photo,
front three-quarter view, hard clean edges, no shadow, no text
```
Founder face (I2I from a real reference photo):
```
Keep the exact identity of this person. Head and neck only, facing camera,
neutral-to-expressive face, isolated on pure white background, photographic,
no hat, no text
```
Then run background removal (`skills/creative/bg-remove-usage.md`) on props and faces.

---

## 9. Production workflow (checklist)

1. **Research** — verify the brand story: founding year, founders, first product, first sales number, the multiplier event, the latest valuation/acquisition. ≥ 2 sources each. Capture 3–5 "surprising" facts; pick the best seed for the hook.
2. **Script** — fill the §3 template; 130–160 words; read-aloud timing check. Present to the user for approval.
3. **Beat sheet / scene plan** — one row per caption group: time, voiceover words, background, characters + face, props, camera move (§5), SFX, caption text/colour. Aim for 18–28 rows.
4. **Assets** — backgrounds (8–12), props, faces (2–4 people), music, SFX. Announce provider + cost before generating; sample 1–2 images first, then batch on approval.
5. **Voice** — generate narration, get word timestamps (TTS alignment or `transcriber`), re-time the beat sheet to real speech.
6. **Compose** — HyperFrames/Remotion, 1080×1920, 30 fps. Camera wrapper per scene, stepped stick-figure poses, caption track, counters.
7. **Mix + render** — voice/music/SFX levels per §7, -14 LUFS.
8. **Review** — §10 checklist + `skills/meta/reviewer.md`. Extract frames every 1 s and look at them.

---

## 10. Quality gate (must all pass before delivery)

- [ ] Frame 0 shows the year; the seed is understood by 2 s.
- [ ] Duration 45–60 s; script 130–160 words; ends on the punchline with nothing after.
- [ ] No shot holds longer than 3 s without a prop pop, camera move or caption change.
- [ ] Founder faces recognisable; stick bodies are red; at least one meme face appears.
- [ ] Every number is on screen as a counter/chart or coloured caption.
- [ ] Captions word-synced (±80 ms), inside the safe zone, never covering a face.
- [ ] ≥ 1 SFX per beat; voice always intelligible over music; -14 LUFS ± 1.
- [ ] No camera move reveals a plate edge; no out-in pumping between adjacent shots.
- [ ] Facts verified; numbers softened where sources disagree.
- [ ] Title follows `How <Brand> Was Founded <emoji> #shorts #business`.

---

## 11. Topic bank

Already covered by the reference channel (avoid exact repeats or find a new angle):
Gillette, Casio, Liquid Death, Rockstar Energy, Dyson, Panasonic, Koenigsegg, Ryanair,
John Deere, MSI, Scrub Daddy, Warby Parker, Twix, Chupa Chups, Activision, Glock,
Swarovski, Zoom, Louis Vuitton, Heckler & Koch, Swatch, Steam, JetBlue, Honda,
Yamaha, 7-Eleven, YETI, Richard Mille, Bank of America, Toyota, BIC, Emirates,
Rheinmetall, Expedia, Bacardi, 3M, Aldi, AMD, Chobani, Standard Oil, Arizona,
Marlboro, Wrigley, Hard Rock Cafe, MINI, Sega, IKEA, Nvidia, Häagen-Dazs, Canon.

Strong next candidates (high brand recognition + a weird seed):
Nike (waffle-iron sole, sold shoes from a car trunk), Red Bull (Thai energy tonic),
Lego (wooden ducks after a fire), Nintendo (playing cards, 1889), Samsung (dried fish
and noodles), Nokia (paper mill), Play-Doh (wallpaper cleaner), WD-40 (40th attempt),
Rolex, Ferrari vs Lamborghini (tractor insult), Coca-Cola, Dr Pepper, Tabasco, Monopoly.
