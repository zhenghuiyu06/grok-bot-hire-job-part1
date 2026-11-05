# Grok Bot Part1 — Hire a job, not a task (Nico material pack)

Public clone (placeholder until the empty public repo exists and is pushed):

```text
https://github.com/zhenghuiyu06/grok-bot-hire-job-part1
```

Original-quality X/demo clips + locked VO + shot correspondence for the episode
**Hire a job, not a task** (Part 1 of the Grok Bot “hire” series). Media under `raw/` is
**byte-identical to the source downloads** — no re-encode, no recompress for this upload.

## What is in this repo

| Path | Contents |
|------|----------|
| `raw/*.mp4` | **Original HQ MP4s** (Git LFS). ~301 MiB across 35 clips. Largest ~63 MiB. |
| `VO_LOCKED.md` | Locked English VO for the episode |
| `SHOT_CORRESPONDENCE.md` | Beat → clip / still mapping |
| `BEATS_S01_S12.md` | Beat sheet S01–S12 |
| `DYNAMIC_INDEX.md` | Dynamic clip index |
| `probe_raw.tsv` | FFprobe summary of every `raw/` file |
| `RIGHTS.md` / `SHORTLIST.md` / `GAPS.md` | Rights notes, shortlist, known gaps |
| `AUDIENCE_MATCH_BRIEF.md` / `TITLE.md` / `LOCK.md` | Briefing + lock state |
| `stills/` | Author / UI stills (PNG/WebP) |
| `en_cards/` | On-screen EN card copy |
| `sources/` | Saved HTML source pages + notes |
| `docs/` | Extra public-doc URL notes |
| `MANIFEST.sha256` | SHA-256 of every `raw/*.mp4` and key docs |
| `CLAUDE.md` | **Mandatory** quality rules for Claude Code / editors |

Not included (on purpose): Claude handoff `tar.gz` / zip packs, oversized split recompressions,
and any proxy/preview encodes. Prefer `raw/` only.

## Claude Code — how to use this repo

1. **Clone with Git LFS** (required for real video bytes):

   ```bash
   git lfs install
   git clone https://github.com/zhenghuiyu06/grok-bot-hire-job-part1.git
   cd grok-bot-hire-job-part1
   git lfs pull   # if objects were not fetched during clone
   ```

2. **Never use LFS pointer files as video.** A pointer is a tiny text file starting with
   `version https://git-lfs.github.com/spec/v1`. Real MP4s are multi-MB binaries. If
   `wc -c raw/*.mp4` shows ~130 bytes, run `git lfs pull`.

3. **Verify integrity** against the committed manifest:

   ```bash
   sha256sum -c MANIFEST.sha256
   ```

4. **Obey the quality protection rules** (also in `CLAUDE.md`):

   1. 从 Git LFS 获取完整原始 MP4，不得使用指针文件代替视频。
   2. 下载后验证文件完整性。
   3. 保留原视频分辨率、帧率和尽可能高的画质。
   4. 可无损剪切的片段优先使用 stream copy。
   5. 必须重新编码时，优先使用高质量编码参数。
   6. 禁止无必要的降分辨率、虚假升帧和过度压缩。
   7. 导出后使用 FFprobe 对比原始素材与成片的参数。
   8. 禁止使用低清预览版本代替原始素材。

## Direct media tip

After a successful `git lfs pull`, open files under **`raw/`**. Do not dig in pack zips or
preview folders for “lighter” substitutes.

## Local staging note

This tree was prepared as a GitHub-ready stage: originals hardlinked from the episode
workspace, LFS attributes set, manifest written. Push requires a public empty repo at the
URL above and a working GitHub credential on the pushing machine.
