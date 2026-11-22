# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 148.39 ± 0.22 | 169.50 ± 0.14 | -12.45% | 41.79 ± 0.06 | 41.65 ± 0.05 | +0.33% |
| 256 | 147.65 ± 0.32 | 169.40 ± 0.24 | -12.84% | 40.73 ± 0.07 | 40.87 ± 0.05 | -0.33% |
| 512 | 146.90 ± 0.12 | 167.57 ± 0.68 | -12.33% | 38.77 ± 0.06 | 40.22 ± 0.06 | -3.62% |
| 1024 | 144.59 ± 0.15 | 165.47 ± 0.71 | -12.62% | 35.13 ± 0.08 | 39.10 ± 0.05 | -10.15% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
