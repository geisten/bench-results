# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 17.72 ± 0.10 | 26.73 ± 0.37 | -33.70% | 4.13 ± 0.04 | 3.51 ± 0.03 | +17.69% |
| 256 | 17.29 ± 0.14 | 23.51 ± 0.84 | -26.45% | 4.07 ± 0.06 | 3.40 ± 0.05 | +19.76% |
| 512 | 16.94 ± 0.13 | 24.25 ± 0.81 | -30.16% | 4.03 ± 0.06 | 3.34 ± 0.10 | +20.64% |
| 1024 | 16.37 ± 0.04 | 23.30 ± 1.23 | -29.76% | 3.95 ± 0.03 | 3.27 ± 0.02 | +20.88% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
