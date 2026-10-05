---
name: opuscar-social
description: Direct and produce a short social media video (TikTok, Instagram Reels, YouTube Shorts, LinkedIn, X) made entirely in code, with captions, voice, music and a ready-to-paste post pack. Use when the user asks for a reel, short, TikTok, social video, promo clip, explainer, ad, tutorial video, listicle, or any short-form video, whether or not they name a style; also for a cinematic film style from the library. Not for editing or converting existing video files.
---

# Opuscar Social

The styles, guides and tools live in the Opuscar Social library (github.com/aroramit17/lemo-opuscar, a social-video fork of lemomo-ai/lemo-opuscar). This skill fetches it and hands you over to it.

1. **Get the library.** Run `sh "<skill base directory>/scripts/setup.sh"`. It clones or updates the library (default `~/lemo-opuscar`; a clone the user is standing in is used as it is) and prints `LIB=<path>` on its last line.
2. **Install the core tools early.** Start `sh "<skill base directory>/scripts/setup.sh" deps` right away, in the background if you can: it takes a few minutes the first time. Add `deps voice` or `deps music` later, only if the film needs them (`$LIB/TECHNIQUE.md` §1). Report missing system tools in your one round of questions; don't install system software yourself.
3. **Follow the library.** Read `$LIB/AGENTS.md`, then `$LIB/SOCIAL.md` for any short-form video, and do what they say: choosing a style from `$LIB/social/README.md`, the one round of questions, the treatment, production and delivery. Social defaults: 1080x1920, 30 fps, burned-in captions, `cover.jpg`, `.srt` and `POST.md`.

What changes in skill mode:

| | |
|---|---|
| Project folder | `<name>/` in the folder the user started from (lowercase letters, digits, hyphens; avoid `#` and `?` in the path). Wherever the guides say `films/<name>/`, read this folder |
| Running tools | from `$LIB`, with the project's absolute path: `cd "$LIB" && node core/render/still.mjs "<project>" 1.5 3` |
| Library files in pages | absolute URLs: `/core/lib.js`, `/node_modules/three/…` (the project is served at `/@film/`) |
| Library files in scripts and `build.sh` | `$LIB/…`, with `LIB=<path>` at the top of `build.sh`; never `../..` |
| Demo source | not downloaded. `sh "<skill base directory>/scripts/setup.sh" demo <slug>`, only after your `TREATMENT.md` is written, to read its techniques; it is not meant to be rendered |

Deliver what `$LIB/SOCIAL.md` §11 lists (for a cinematic film, `$LIB/DIRECTOR.md` §11), in the project folder, and tell the user where it is.
