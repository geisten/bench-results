# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 17.82 ± 0.08 | 26.52 ± 0.81 | -32.82% | 4.15 ± 0.04 | 3.55 ± 0.04 | +17.01% |
| 256 | 17.39 ± 0.06 | 24.78 ± 1.31 | -29.81% | 4.10 ± 0.04 | 3.53 ± 0.05 | +16.14% |
| 512 | 16.99 ± 0.07 | 23.90 ± 1.53 | -28.91% | 4.07 ± 0.02 | 3.45 ± 0.04 | +18.01% |
| 1024 | 16.47 ± 0.09 | 23.57 ± 1.47 | -30.15% | 3.96 ± 0.03 | 3.33 ± 0.02 | +18.91% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
