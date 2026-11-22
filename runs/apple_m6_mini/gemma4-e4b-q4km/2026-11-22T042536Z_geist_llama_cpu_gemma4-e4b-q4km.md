# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 177.46 ± 0.12 | 142.69 ± 0.08 | +24.37% | 36.86 ± 0.02 | 34.35 ± 0.01 | +7.31% |
| 256 | 175.72 ± 0.15 | 141.60 ± 0.27 | +24.10% | 36.27 ± 0.06 | 33.50 ± 0.02 | +8.28% |
| 512 | 171.40 ± 0.18 | 142.06 ± 0.54 | +20.65% | 35.19 ± 0.06 | 33.02 ± 0.01 | +6.58% |
| 1024 | 166.65 ± 0.14 | 136.86 ± 0.42 | +21.77% | 34.46 ± 0.04 | 32.31 ± 0.02 | +6.65% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
