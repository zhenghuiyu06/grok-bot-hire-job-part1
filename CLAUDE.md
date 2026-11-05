# Claude Code — video quality protection rules

This repository contains **original-quality** MP4 source clips for the Nico-style episode
**Grok Bot Part1 — Hire a job, not a task**. Treat every file under `raw/` as camera-original
(or as-downloaded HQ). Do **not** substitute LFS pointer stubs, low-res previews, or re-encoded
proxies for editing.

## How to fetch real video (Git LFS)

```bash
git lfs install
git clone https://github.com/zhenghuiyu06/grok-bot-hire-job-part1.git
cd grok-bot-hire-job-part1
# If clone skipped LFS objects:
git lfs pull
```

Verify you have real MP4s, not pointer files:

```bash
# Pointer files are tiny (~100–200 bytes) and start with "version https://git-lfs.github.com/spec/v1"
head -c 100 raw/D01_RobautoAI_teach_task.mp4
# Expect binary / ftyp… NOT a text LFS pointer

sha256sum -c MANIFEST.sha256
```

Direct media after a successful LFS pull lives under `raw/`.

---

## 画质保护规则（必须遵守）

1. 从 Git LFS 获取完整原始 MP4，不得使用指针文件代替视频。
2. 下载后验证文件完整性。
3. 保留原视频分辨率、帧率和尽可能高的画质。
4. 可无损剪切的片段优先使用 stream copy。
5. 必须重新编码时，优先使用高质量编码参数。
6. 禁止无必要的降分辨率、虚假升帧和过度压缩。
7. 导出后使用 FFprobe 对比原始素材与成片的参数。
8. 禁止使用低清预览版本代替原始素材。

---

## Quality protection rules (English equivalents)

1. Fetch the full original MP4 via Git LFS; never use an LFS pointer file as the video.
2. After download, verify file integrity (use `MANIFEST.sha256` / `sha256sum -c`).
3. Preserve the original resolution, frame rate, and the highest practical quality.
4. Prefer stream copy (`ffmpeg -c copy`) for lossless cuts when the edit allows it.
5. When re-encode is required, use high-quality encode settings (high bitrate / CRF, matching or better than source).
6. Do not unnecessarily downscale, fake frame-rate upconversion, or over-compress.
7. After export, compare source vs deliverable with FFprobe (resolution, fps, codec, bitrate, duration).
8. Never substitute a low-resolution preview for the original media.

---

## Suggested FFprobe compare (rule 7)

```bash
ffprobe -hide_banner -show_streams -show_format raw/SOURCE.mp4
ffprobe -hide_banner -show_streams -show_format OUT.mp4
```

Check: width/height, r_frame_rate, codec_name, bit_rate, duration. Flag any silent downscale or heavy recompress.

## Editing notes

- Preferred cut: `ffmpeg -ss IN -to OUT -i raw/CLIP.mp4 -c copy -avoid_negative_ts make_zero CLIP_cut.mp4`
- Only re-encode when filters, speed changes, or format constraints require it.
- Source probe table for this pack: `probe_raw.tsv`
- Shot → clip map: `SHOT_CORRESPONDENCE.md`
- Locked VO: `VO_LOCKED.md`
