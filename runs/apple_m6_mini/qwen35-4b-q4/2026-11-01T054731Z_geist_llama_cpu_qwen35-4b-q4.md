# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 148.72 ± 0.21 | 169.35 ± 0.27 | -12.19% | 44.15 ± 0.12 | 41.84 ± 0.02 | +5.51% |
| 256 | 148.20 ± 0.14 | 170.10 ± 0.14 | -12.87% | 43.04 ± 0.06 | 41.09 ± 0.09 | +4.76% |
| 512 | 147.01 ± 0.17 | 167.29 ± 1.23 | -12.12% | 40.83 ± 0.06 | 40.48 ± 0.13 | +0.86% |
| 1024 | 144.62 ± 0.17 | 164.51 ± 0.50 | -12.10% | 36.45 ± 0.33 | 39.28 ± 0.07 | -7.20% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
