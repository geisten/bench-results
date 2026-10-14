# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `db8314e2a3a3`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 56.85 ± 0.20 | 131.03 ± 0.34 | -56.61% | 13.73 ± 0.06 | 11.84 ± 0.06 | +15.91% |
| 256 | 55.40 ± 0.03 | 115.05 ± 0.34 | -51.85% | 13.68 ± 0.05 | 12.34 ± 0.07 | +10.91% |
| 512 | 54.26 ± 0.06 | 110.11 ± 0.61 | -50.73% | 13.58 ± 0.08 | 11.74 ± 0.05 | +15.69% |
| 1024 | 52.93 ± 0.05 | 107.67 ± 0.93 | -50.84% | 13.31 ± 0.09 | 11.47 ± 0.02 | +16.11% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
