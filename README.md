# Opuscar Social

**Short-form social videos, made entirely in code by your coding agent.**
Pick a job (teach, sell, entertain, prove, loop), bring your idea, and let the agent write the hook, captions, voice, music and post copy, then render it vertical-ready for TikTok, Instagram Reels, YouTube Shorts, LinkedIn and X.

This is a fork of [lemomo-ai/lemo-opuscar](https://github.com/lemomo-ai/lemo-opuscar) (MIT), a Claude Code skill that makes films with no video model: canvas and WebGL pages rendered frame by frame, original music from free sample libraries, text-to-speech narration. This fork keeps that engine and retargets it at social media.

## What's different from upstream

| | Upstream | Opuscar Social |
|---|---|---|
| Default output | 1920x1080, 24 fps, cinematic short film | **1080x1920, 30 fps, 20-45 s social video** |
| Styles | 43 art-direction film styles | **10 social styles chosen by job**, plus the original 43 as an optional look |
| Success test | Sound, rhythm, camera, directing | **Hook, retention, sound-off readability, payoff, loop/CTA** |
| Captions | Optional subtitles | **Burned-in, word-timed kinetic captions** inside the safe zone |
| Deliverables | `.mp4`, poster, `.srt` | `.mp4`, **`cover.jpg`, `.srt`, `POST.md`** (caption, hashtags, first comment, alt text), extra presets (4:5, 1:1, 16:9) |

## The ten social styles

| Style | Job |
|---|---|
| [Kinetic Captions](social/kinetic-captions.md) | A voice carries the idea; the words become the picture |
| [Listicle Countdown](social/listicle-countdown.md) | "N things" with a numbered spine, built for saves |
| [Product Teaser](social/product-teaser.md) | Problem, one demonstration, one offer |
| [Text Storytime](social/text-storytime.md) | A story told through a fictional chat, notes page or terminal |
| [Tutorial Steps](social/tutorial-steps.md) | How-to with a guiding cursor and numbered steps |
| [Stat Flash](social/stat-flash.md) | One surprising number, one chart, one reaction |
| [Before / After](social/before-after.md) | A transformation reveal that loops |
| [Carousel Reel](social/carousel-reel.md) | LinkedIn-style slides that swipe themselves |
| [Meme Cutaway](social/meme-cutaway.md) | Setup, beat, reaction, with original characters and jokes |
| [Satisfying Loop](social/satisfying-loop.md) | Seamless, sound-led, hypnotic |

Index and "which one should I use?" guide: [`social/README.md`](social/README.md). The social director's guide (hooks, retention, safe zones, captions, sound, loops, the post pack): [`SOCIAL.md`](SOCIAL.md).

## How to use

**Option 1: install the skill (recommended)**

```
claude plugin marketplace add aroramit17/lemo-opuscar
claude plugin install opuscar-social@opuscar-social
```

Then use it from any folder. On first use it downloads the guides, tools and styles to `~/lemo-opuscar`, shared by all your videos. Each video's project goes in the folder you started from.

**Option 2: clone the repo**

```
git clone https://github.com/aroramit17/lemo-opuscar.git
cd lemo-opuscar
claude
```

Videos go into `films/<name>/` inside the repo.

Then say what you want:

> Make a 30-second Kinetic Captions reel for TikTok: "3 things I wish I knew before building my first Salesforce automation." Use my voice recording, captions in yellow.

> Product Teaser for LinkedIn (4:5), 20 seconds, for a CRM-cleanup tool. Hook on the pain of duplicate records.

It asks you once, up front: your platform, your goal and CTA, who or what is on screen, any material you own (voice, logos, fonts), and the language. Then it builds.

## Requirements

Node 20+, ffmpeg and Python 3.11+ (or uv); the agent installs the rest. A video takes an agent roughly 20-45 minutes and a fair amount of tokens.

## What you get

`<name>.mp4`, `cover.jpg`, `<name>.srt`, `POST.md`, `TREATMENT.md`, `CREDITS` and the source with a one-command `build.sh`.

## Notes and honesty rules

- Styles are tuned for Claude Opus; other models may not reproduce them.
- No trending or copyrighted audio, no imitation of existing memes, characters or brands, no fabricated testimonials or statistics. See `SOCIAL.md` §13.
- Platform limits and interface layouts change; the presets in [`social/platforms.json`](social/platforms.json) are conservative defaults. Verify before you publish.

## Credits and licence

Built on **Lemo-Opuscar** by Lemomo / LemoLab ([github.com/lemomo-ai/lemo-opuscar](https://github.com/lemomo-ai/lemo-opuscar)), MIT licensed. All of upstream's engine, tools and cinematic styles are retained; the social layer (`SOCIAL.md`, `social/`, and the edits to `AGENTS.md`, the skill and the marketplace file) is new in this fork. See `LICENSE`. Third-party assets in the demos keep their own licences; you are responsible for the materials you use in your videos.
