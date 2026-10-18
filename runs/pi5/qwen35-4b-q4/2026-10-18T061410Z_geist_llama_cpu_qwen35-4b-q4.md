# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 17.59 ± 0.24 | 27.44 ± 0.11 | -35.90% | 4.53 ± 0.08 | 3.58 ± 0.03 | +26.65% |
| 256 | 17.19 ± 0.13 | 26.08 ± 0.69 | -34.10% | 4.40 ± 0.07 | 3.49 ± 0.05 | +25.96% |
| 512 | 16.81 ± 0.18 | 25.20 ± 0.83 | -33.28% | 4.39 ± 0.03 | 3.42 ± 0.07 | +28.45% |
| 1024 | 16.32 ± 0.14 | 24.85 ± 0.84 | -34.33% | 4.31 ± 0.02 | 3.34 ± 0.02 | +29.16% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
