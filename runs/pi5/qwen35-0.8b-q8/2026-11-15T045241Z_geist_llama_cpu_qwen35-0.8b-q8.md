# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.83 ± 0.31 | 128.88 ± 1.30 | -8.58% | 13.59 ± 0.10 | 11.80 ± 0.06 | +15.17% |
| 256 | 110.26 ± 0.42 | 103.37 ± 6.54 | +6.67% | 13.53 ± 0.20 | 11.99 ± 0.28 | +12.91% |
| 512 | 105.68 ± 0.23 | 103.18 ± 6.35 | +2.42% | 13.41 ± 0.18 | 11.70 ± 0.04 | +14.67% |
| 1024 | 100.74 ± 0.20 | 101.12 ± 6.41 | -0.37% | 13.10 ± 0.16 | 11.37 ± 0.09 | +15.23% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
