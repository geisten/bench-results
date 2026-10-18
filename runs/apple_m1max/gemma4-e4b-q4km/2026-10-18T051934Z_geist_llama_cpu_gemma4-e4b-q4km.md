# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 93.31 ± 0.04 | 154.61 ± 1.66 | -39.65% | 26.44 ± 0.12 | 27.05 ± 0.07 | -2.25% |
| 256 | 90.33 ± 1.27 | 154.56 ± 2.12 | -41.56% | 24.49 ± 0.04 | 26.62 ± 0.15 | -8.03% |
| 512 | 81.22 ± 0.98 | 152.11 ± 6.07 | -46.60% | 21.08 ± 0.07 | 26.25 ± 0.06 | -19.69% |
| 1024 | 75.93 ± 0.41 | 144.92 ± 3.62 | -47.61% | 19.08 ± 0.11 | 25.91 ± 0.19 | -26.36% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
