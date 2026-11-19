# Zingers

**A reply-first social platform concept for comment-section humor, with a clickable prototype and a pilot study on how much context a reply needs.**

Course project for a social media course at Rutgers University (Fall 2026). Status: research in progress; prototype and pilot survey complete, pilot data collection under way.

---

## The idea

On TikTok, some of the funniest content is not the video but the comments under it, where strangers build instant inside jokes. That humor lives in a thread beneath someone else's post, so it is hard to browse and its authors are rarely credited.

Zingers turns that comment-section wit into its own platform. The unit of the feed is not the post. It is the **reply card**: a reply paired with a one-line **context chip** that quotes the prompt it answers. Replies from different prompts are ranked together in one feed, and each user has a **wit record** that collects their best replies across prompts. Prompts are capped at one line of text or one image, so they are cheap to carry along with the reply.

### The design tension

The concept started from a question that any comment-first app has to answer:

- If you remove the original post and show only replies, many replies become illegible.
- If you keep the original post, the app looks like Reddit or YouTube.

### Thesis

> A reply needs only a small, bounded amount of its prompt to stand on its own, so carrying that context with the reply lets a platform rank and credit replies across prompts without becoming a thread viewer.

## Research questions

| | Question |
|---|---|
| **RQ1** | How much of a prompt (none, a one-line chip, or the full prompt) do readers need to understand and enjoy a reply? |
| **RQ2** | Does a reply-card feed or thread browsing better help people find funny replies? |
| **RQ3** (exploratory) | How do people expect identity and moderation to work on a humor-first platform? |

## What is in this repository

```
zingers/
├── README.md                 This file
├── figma-plugin/             Generates the clickable prototype in Figma
│   ├── manifest.json
│   ├── code.js
│   └── README.md
├── pilot-study/              The rating survey used in the pilot
│   └── index.html            Self-contained page, no build step
├── figures/                  Prototype figures used in the paper
│   ├── fig1_context_versions.png
│   └── fig2_other_screens.png
├── paper/                    Preliminary draft (ACM template)
│   └── Zingers_Preliminary_Draft.docx
└── data/                     Anonymous pilot responses, one JSON object per line
    └── pilot_responses.jsonl
```

Adjust the folder names to match how you lay the repo out.

## 1. The prototype (Figma plugin)

`figma-plugin/` is a Figma plugin that builds the whole prototype as editable frames with real prototype connections, so it can be changed, clicked through, and exported.

**Screens (7 frames, 390 x 844):**

| Frame | What it shows |
|---|---|
| 1b Feed: context chip (default) | Reply cards from different prompts, each with a one-line chip quoting its prompt |
| 1a Feed: no context | Study condition: reply, handle and votes only |
| 1c Feed: full prompt | Study condition: the whole prompt above each reply |
| 2 Thread view | Full prompt with its replies ranked; opened by tapping a card |
| 3 Reply | Shows the chip the reply will carry |
| 4 Post a prompt | 140-character cap |
| 5 Profile and wit record | Stats across prompts and best replies with their chips |

A toggle at the top of the feed switches between the three context versions. A tab bar (Feed, Post, Profile) or a Back control is on every screen, so there are no dead ends.

**Run it:**
1. In the Figma desktop app, open a Design file.
2. Plugins > Development > Import plugin from manifest, then choose `figma-plugin/manifest.json`.
3. Run Plugins > Development > Zingers Prototype Generator.
4. Select any frame and press Present to click through.

To use different stimuli, edit the `ITEMS` list at the top of `code.js` and rerun. The plugin creates new frames on each run, so delete old ones first. To export figures for a paper, select frames and use Export (PNG, 2x).

Tech: Figma Plugin API (frames, text, rectangles, `setReactionsAsync` for navigation, flow starting points). The figures in `figures/` were rendered from the plugin's layout with a local script, so fonts differ slightly from what Figma shows.

## 2. The pilot study (rating survey)

`pilot-study/index.html` is a single-page web survey that tests RQ1 in a within-subjects design.

**Design**
- 4 prompts, 3 replies each, 12 short replies written for the study.
- Every participant rates all 12 replies. Four appear with no context, four with a context chip, four with the full prompt.
- Conditions rotate across three versions (A, B, C) so every reply appears in every condition across participants, and every prompt appears in every condition once per participant.
- For each reply: comprehension (1 to 5) and funniness (1 to 5).
- Exit questions: clearest version, feed-versus-thread preference (RQ2), comment-section habits, and how people want their name shown on a platform like this (RQ3). One optional comment box.

**Privacy**
- No name, email or account. Nothing is sent to a server.
- At the end, the participant copies a block of JSON and sends it to the researcher.

**Run it:** open `index.html` in a browser, or publish it with GitHub Pages (Settings > Pages > deploy from `main`, root). Each visitor is randomly assigned a rotation. Add `#a`, `#b` or `#c` to the URL to force one.

**Analysis plan:** compare mean comprehension and funniness across the three conditions descriptively and report the sample size. With a small convenience sample, results are indicative, not generalizable.

## 3. The paper

`paper/` holds the preliminary draft in the ACM small template: Introduction, Related Work, Methods, Findings, Contributions and References. Findings are limited to what has actually been gathered. Pilot results are added from the real responses in `data/`.

Planned final paper: 12 to 15 pages in an academic article style, with at least 20 references.

## Status

| Piece | Status |
|---|---|
| Literature review (12 sources) | Done |
| Feature comparison with other platforms | Done, table cells still to be verified |
| Clickable prototype (7 frames) | Done |
| Pilot survey | Built; data collection in progress |
| Pilot analysis | Pending responses |
| Preliminary draft | Written; pilot findings pending |

## Limitations

- The stimuli were written by the researcher, not sampled from real comment sections.
- The pilot uses a small convenience sample, so results are indicative only.
- The prototype is low fidelity and has no real ranking, accounts or moderation.
- Replies are rated one at a time, which does not test finding a funny reply in a live feed (RQ2).

## Roadmap

- Larger pilot and a pre-planned analysis.
- Replace the written stimuli with real public comment examples, with permission.
- A feed-browsing task to test RQ2 directly against a thread view.
- Interviews on identity and moderation for RQ3.

## Related work

This project draws on research on humor and community on TikTok, humor and harm, anonymous vote-ranked apps such as Yik Yak, and context collapse. See the paper for the full reference list. Key sources include:

- Matamoros-Fernandez. 2023. Taking humor seriously on TikTok. *Social Media + Society*.
- Schaadhardt, Fu, Pratt, and Pratt. 2023. "Laughing so I don't cry". *CHI '23*.
- Newton, Zappavigna, Drysdale, and Newman. 2022. More than humor: Memes as bonding icons for belonging in donor-conceived people. *Social Media + Society*.
- Saveski, Chou, and Roy. 2016. Tracking the Yak. *ICWSM*.
- Bayne et al. 2019. The social value of anonymity on campus: A study of the decline of Yik Yak. *Learning, Media and Technology*.
- Marwick and boyd. 2011. I tweet honestly, I tweet passionately. *New Media & Society*.

## Author

**[Your name]**, [your institution]. [Link to portfolio or LinkedIn]

## License

Code: MIT. Written material and figures: CC BY 4.0. Change these if your course or instructor requires something else.
