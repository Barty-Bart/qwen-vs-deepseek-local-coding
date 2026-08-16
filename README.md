# Qwen 3.8 27B vs DeepSeek V4 Flash — local coding tests

Same prompts, same machine, same day. Everything ran locally.

| | Model | Size | Active/token | Memory | Speed |
|---|---|---|---|---|---|
| **Qwen** | Qwen3.8-27B 8-bit | 27B dense | 27B | 31 GB | 44 tok/s |
| **DeepSeek** | DeepSeek-V4-Flash-0731 MXFP4 | 305B MoE | ~13B | 175 GB | 38 tok/s |

Mac Studio M3 Ultra, 80-core GPU, 512GB unified memory. Served by
[oMLX](https://github.com/jundot/omlx) 0.5.7 on MLX 0.32.0, driven through the
**pi** coding agent so each model writes and reads its own files.

DeepSeek runs at its native trained precision (MXFP4). Qwen is the one that has
been quantised, from bf16 down to 8-bit.

## Tests

| | Task | Result |
|---|---|---|
| [01](01-easy-weather-dashboard/) | Weather dashboard, Open-Meteo API | both work |
| [02](02-medium-tower-defense/) | Tower defence game on canvas | both work |
| [03](03-hard-spreadsheet/) | Spreadsheet with a formula engine | see notes |

Each folder has the exact `prompt.md` both models were given and their raw
output. Open the `.html` files directly in a browser.

## Timings

| Test | DeepSeek | Qwen |
|---|---|---|
| 01 weather | 2m 17s, 3 turns | 7m 48s, 7 turns |
| 02 tower defence | 4m 12s, 10 turns | 6m 01s, 7 turns |
| 03 spreadsheet | 3m 51s, 6 turns | ~14m |

Thinking was **off** for tests 01, 02 and 03. Test 3.1 turns it on — see the
[03 notes](03-hard-spreadsheet/README.md).
