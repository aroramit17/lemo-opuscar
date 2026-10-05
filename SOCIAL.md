# Directing a social video

The social-first layer on top of [`DIRECTOR.md`](DIRECTOR.md) and [`TECHNIQUE.md`](TECHNIQUE.md). Read this first for any short-form request (TikTok, Instagram Reels, YouTube Shorts, LinkedIn, X, Facebook). Where this file and DIRECTOR.md disagree, this file wins for social work; everything it does not mention (benchmark, treatment, sound-first thinking, review loop, copyright red lines) still applies.

A social video is judged in this order: **hook, retention, sound-off readability, payoff, loop/CTA**. A beautiful frame that nobody watches past second two is a failed video.

---

## 1. Take the brief

Ask once, in a single message, and skip whatever the request already answers:

- **Platform and placement**: where will it be posted first? (Defaults to vertical for TikTok, Reels and Shorts; 4:5 or 1:1 for LinkedIn and Facebook feeds; 9:16 or 16:9 for X.)
- **Goal**: one of *follow*, *click*, *sell*, *teach*, *entertain*. One goal per video.
- **The one thing**: the single idea, claim, product or lesson a viewer should walk away with. If there are two, make two videos.
- **Who is on screen**: the user's voice, a TTS narrator, or no voice at all (text and music only). Their own logos, product shots, screen recordings and fonts, if any.
- **CTA**: what the viewer should do at the end (follow, comment a keyword, visit a link in bio, save).
- **Language** for voice and captions (default: the language they write in).

Defaults: **1080×1920, 30 fps, 20–45 s, voice-led, burned-in captions, loudness −14 LUFS.** Say so in your summary of the brief.

## 2. Format presets

| Preset | `--size` | Use for | Typical length |
|---|---|---|---|
| `vertical` | `1080x1920` | TikTok, Reels, Shorts, Stories, X vertical | 15–45 s (hard ceilings differ by platform and change; check before promising a length) |
| `portrait` | `1080x1350` | Instagram feed, LinkedIn feed, Facebook feed | 15–60 s |
| `square` | `1080x1080` | LinkedIn, X, Facebook, fallback everywhere | 15–60 s |
| `landscape` | `1920x1080` | YouTube long form, X, website embeds | 30–90 s |

Machine-readable copy: [`social/platforms.json`](social/platforms.json). Render with `node core/render/video.mjs <project> --fps 30 --size 1080x1920`, and pass `30` as the `fps` argument of `core/render/mux.sh`. Build the page responsive to `innerWidth x innerHeight` from the start so one source renders every preset (section 9).

## 3. Safe zones

Platform interfaces cover the frame (username and caption at the bottom, buttons down the right edge, search and tabs at the top). On a 1080×1920 canvas:

- Keep all text and faces inside the **central safe area**: roughly 64 px from the left, 140 px from the right, 220 px from the top and **400 px from the bottom**.
- The bottom 400 px may hold background only. Burned-in captions sit in the lower-middle band, **above** that line (about y = 1050–1450), never on the bottom edge.
- Put a visible guide overlay in your still-review pages (`?guides=1`) and check it on every key frame. Treat these numbers as a conservative default; interfaces change.

For `portrait` and `square`, keep 6% margins and captions in the lower third.

## 4. The hook (0–3 seconds)

- **Something happens in frame 1.** No logo sting, no fade-in from black, no "hey guys".
- The first 3 seconds contain **one** of: a bold claim, a question the viewer can't answer yet, a visible result ("this took 40 seconds"), a pattern break (impossible motion, extreme close-up, wrong-colour world), or an open loop ("the third one is why it broke").
- The hook must be **readable with the sound off**: big on-screen text of 3–7 words, set on the first frame.
- Write three hook candidates in `TREATMENT.md`, pick one, and say why. Render the hook as a still and look at it at thumbnail size before building anything else.
- Never pay off the hook inside the first 3 seconds, and never abandon it: whatever it promises must arrive.

## 5. Retention structure

- **A change every 1.5–3 s**: a cut, a camera move, a new word group, a new element, a colour shift. Hold longer only for a reveal and mark it with sound.
- **Open loops**: promise something early, deliver it late. Number lists ("3 mistakes") count the viewer down.
- **One idea per beat.** If a beat needs two sentences of voice, split it.
- **Mid-point pattern break** around 40–60% of the length: a style shift, a zoom, a stinger.
- Cut every second that does not move the one thing forward. Under 30 s beats over 45 s unless the content earns it.
- Use `core/render/readcheck.mjs`, with a `--min` of 1.0 for single-word kinetic captions and the defaults for anything a viewer must read as a sentence.

## 6. Captions

Captions are part of the picture, not an afterthought; most viewers start with sound off.

- Word-level timing comes from `asr_check.py` (`words.json`). Build the captions in-page from those timings so they follow the voice exactly.
- 1–4 words at a time for kinetic styles; one short line (≤ 42 characters, ≤ 2 lines) for sentence styles.
- Large: 64–110 px on a 1080-wide canvas, heavy weight, with a stroke, shadow or plate so they read on any background. Contrast first, style second.
- Highlight the **word being spoken** or the one key word per phrase, and never more than one highlight colour.
- Also export an `.srt` (`core/render/srt.py`) so the user can upload it as a separate caption track.

## 7. Sound

- **Voice leads.** Keep it close, dry, a touch fast (Kokoro `speed` 1.0–1.1). Remove breaths and gaps over 0.25 s.
- Music sits **15–20 dB under the voice** and ducks around key words; it carries energy, not melody competing with speech. With no voice, music and sound effects carry the whole timing.
- Sound effects on every on-screen change (a tick per caption pop, a whoosh per cut, a hit on the reveal) are what make short-form feel finished. Use `core/audio/sfx.py`.
- Master to **−14 LUFS** with `mux.sh`. Do not use or imitate trending or copyrighted audio; the user can lay a licensed track over the exported stems if they choose.

## 8. Endings, loops and CTA

- End on the **payoff**, then the CTA in under 2 seconds, and stop. No outro, no fade, no "thanks for watching".
- **Loop when you can**: make the last frame match the first so replays are seamless (same layout, same colour, last word leads back into the first). Looping styles are marked in their `STYLE.md`.
- Spoken CTA and on-screen CTA say the same thing, once. A keyword CTA ("comment GUIDE") beats a vague one.

## 9. One source, many cuts

- Build the page against the canvas size it gets. All layout is computed from `W` and `H`, not hard-coded to 1080×1920.
- Deliver the primary preset plus, if the user posts on more than one platform, the other presets as extra renders from the same source. Re-check safe zones for each.
- If asked for A/B tests, vary **only the hook** (the first 3 seconds) between versions, and name the files `<name>-hookA.mp4`, `<name>-hookB.mp4`.

## 10. Style choice

Pick from [`social/README.md`](social/README.md). Match the style to the **job** (teach, sell, argue, entertain), not to what looks coolest. The ten social styles are built for the formats above; the 43 cinematic film styles in `styles/` can still be used for a social video when the user names one, in which case apply sections 3–9 of this file on top.

## 11. Before you deliver

- Watch it once at full speed **with sound off**: can you still follow it? Once more **with sound on, on a phone-sized view** (resize your player to about 390 px wide).
- The first 3 seconds, as a still, make a promise at thumbnail size.
- Every on-screen text is inside the safe zone on every preset delivered; readcheck passes.
- No dead air over 0.3 s, no static frame over 3 s without a reason, no black or NaN frames.
- Voice transcribes back correctly (`asr_check.py`); loudness about −14 LUFS; loop point is clean if the style loops.
- No LemoLab or upstream sign-off or watermark: the video belongs to the user.

**Deliver**, in the project folder:

- `<name>.mp4` (the primary preset) and any other preset renders;
- `cover.jpg`: the single best frame, pulled at a moment where the text is fully visible, for use as the cover/thumbnail;
- `<name>.srt`;
- `POST.md`: a ready-to-paste **post pack** (section 12);
- `TREATMENT.md`, `CREDITS`, and the source with a one-command `build.sh`.

## 12. The post pack (`POST.md`)

Short, copy-ready, in the video's language:

1. **Caption**: first line is the hook restated; 1–3 short lines; the CTA last.
2. **On-screen text for the cover** (≤ 6 words).
3. **Hashtags / keywords**: 3–6 that describe the topic, no filler.
4. **First comment**: one line that adds value or asks a question the video leaves open.
5. **Alt text** (one sentence) and, where the platform asks for it, a title (≤ 70 characters).
6. **Posting note**: which preset to upload where.

## 13. Copyright and honesty

Everything in [`DIRECTOR.md`](DIRECTOR.md) §12 applies. In addition: no fabricated testimonials, fake screenshots of real people or brands, invented statistics, or fake "results" presented as real. Stat and claim styles show numbers the user supplied or can source; put the source in `CREDITS` and, when it fits, on screen. Label dramatizations as such.
