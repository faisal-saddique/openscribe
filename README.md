# OpenScribe

Free video transcription with OpenAI's Whisper **large-v3**, running on your own
Google Colab GPU.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/faisal-saddique/openscribe/blob/main/OpenScribe.ipynb)

There is no server. You open the notebook, click Run, and it executes on the free
T4 that Google already gives you. Your video goes from your machine — or straight
from a link — into your own Colab runtime, and never passes through infrastructure
belonging to anyone else.

## What it does

| | |
|---|---|
| **Model** | Whisper `large-v3`, beam size 5 (`large-v3-turbo`, `large-v2`, `medium.en`, `small.en` also available) |
| **Speed** | 8–12× real time on a free T4 — an hour of audio in 5–8 minutes |
| **Input** | File upload, Google Drive, or any direct link (Discord CDN attachments, S3, Dropbox); falls back to `yt-dlp` for YouTube and similar |
| **Output** | `.txt` `.srt` `.vtt` `.tsv` `.json` with word-level timestamps and per-segment confidence |
| **Backends** | `faster-whisper` by default, with automatic fallback to reference `openai-whisper` |

Every setting is a Colab form control — model, language, beam size, subtitle line
width — so you never have to edit code.

## Known limits

- **No speaker labels.** Whisper doesn't do diarisation. Word timestamps are in the
  JSON if you want to align a diarisation model against them.
- **Colab's free tier disconnects.** Long jobs get reclaimed at busy times. Past
  ~2 hours of audio, use `large-v3-turbo` or Colab Pro.
- **Whisper hallucinates over silence.** VAD filtering suppresses most of it and the
  quality-check cell flags what's left, but skim the output before trusting it.

## Running it elsewhere

Nothing in the notebook is Colab-specific except the upload and Drive helpers. On
your own machine:

```bash
pip install -U faster-whisper yt-dlp
```

…then lift the transcription and writer cells straight out.

## Licence

MIT. Whisper is by [OpenAI](https://github.com/openai/whisper); the fast backend is
[faster-whisper](https://github.com/SYSTRAN/faster-whisper) by SYSTRAN.

If it saved you an afternoon, you can [buy me a coffee](https://buymeacoffee.com/faisalsaddique).
