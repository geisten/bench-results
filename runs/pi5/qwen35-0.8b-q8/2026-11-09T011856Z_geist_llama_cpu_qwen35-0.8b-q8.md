# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.90 ± 0.18 | 131.65 ± 0.60 | -10.44% | 13.77 ± 0.05 | 12.35 ± 0.09 | +11.45% |
| 256 | 110.54 ± 0.18 | 114.71 ± 0.53 | -3.64% | 13.75 ± 0.07 | 12.37 ± 0.07 | +11.21% |
| 512 | 105.85 ± 0.30 | 110.58 ± 0.13 | -4.28% | 13.66 ± 0.07 | 11.74 ± 0.03 | +16.28% |
| 1024 | 101.01 ± 0.10 | 107.63 ± 0.18 | -6.15% | 13.28 ± 0.09 | 11.48 ± 0.06 | +15.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
