# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 148.44 ± 0.21 | 169.40 ± 0.23 | -12.37% | 41.27 ± 0.10 | 41.09 ± 0.07 | +0.43% |
| 256 | 148.08 ± 0.19 | 170.15 ± 0.22 | -12.97% | 40.29 ± 0.16 | 40.29 ± 0.08 | -0.02% |
| 512 | 147.02 ± 0.13 | 168.38 ± 0.21 | -12.69% | 38.39 ± 0.02 | 39.72 ± 0.04 | -3.35% |
| 1024 | 144.70 ± 0.12 | 165.88 ± 0.38 | -12.77% | 34.27 ± 0.28 | 38.58 ± 0.13 | -11.16% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
