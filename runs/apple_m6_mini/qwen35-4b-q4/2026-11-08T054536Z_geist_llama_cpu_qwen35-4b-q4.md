# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 148.64 ± 0.10 | 169.50 ± 0.20 | -12.30% | 41.13 ± 0.14 | 40.90 ± 0.13 | +0.54% |
| 256 | 147.88 ± 0.21 | 170.37 ± 0.12 | -13.21% | 40.33 ± 0.09 | 40.19 ± 0.11 | +0.34% |
| 512 | 146.96 ± 0.09 | 168.59 ± 0.06 | -12.83% | 38.36 ± 0.12 | 39.79 ± 0.09 | -3.58% |
| 1024 | 144.87 ± 0.11 | 166.31 ± 0.10 | -12.89% | 34.86 ± 0.06 | 38.70 ± 0.10 | -9.94% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
