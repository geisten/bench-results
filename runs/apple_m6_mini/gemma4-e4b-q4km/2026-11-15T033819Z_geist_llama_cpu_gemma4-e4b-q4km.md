# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 178.06 ± 0.15 | 142.59 ± 0.10 | +24.88% | 36.29 ± 0.01 | 33.90 ± 0.06 | +7.06% |
| 256 | 176.22 ± 0.07 | 141.61 ± 0.40 | +24.44% | 35.77 ± 0.05 | 33.07 ± 0.08 | +8.18% |
| 512 | 171.89 ± 0.07 | 142.04 ± 0.29 | +21.01% | 34.77 ± 0.02 | 32.65 ± 0.06 | +6.50% |
| 1024 | 167.17 ± 0.10 | 136.84 ± 0.34 | +22.17% | 34.05 ± 0.03 | 31.99 ± 0.07 | +6.44% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
