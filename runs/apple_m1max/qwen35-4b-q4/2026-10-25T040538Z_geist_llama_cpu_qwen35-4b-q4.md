# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 167.99 ± 0.49 | 192.90 ± 1.06 | -12.92% | 36.48 ± 0.09 | 32.93 ± 0.18 | +10.79% |
| 256 | 167.15 ± 0.38 | 190.12 ± 1.49 | -12.08% | 35.62 ± 0.06 | 32.85 ± 0.22 | +8.42% |
| 512 | 163.57 ± 1.27 | 191.81 ± 4.32 | -14.72% | 33.75 ± 0.08 | 32.35 ± 0.35 | +4.32% |
| 1024 | 155.01 ± 2.26 | 183.66 ± 4.97 | -15.60% | 30.07 ± 0.16 | 32.04 ± 0.06 | -6.15% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
