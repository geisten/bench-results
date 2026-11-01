# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1279.64 ± 2.06 | 1310.55 ± 3.34 | -2.36% | 46.15 ± 0.01 | 45.49 ± 0.03 | +1.43% |
| 256 | 1358.84 ± 2.61 | 1419.78 ± 0.78 | -4.29% | 46.01 ± 0.01 | 45.23 ± 0.08 | +1.74% |
| 512 | 1356.42 ± 1.61 | 1402.09 ± 1.03 | -3.26% | 45.66 ± 0.01 | 45.06 ± 0.10 | +1.35% |
| 1024 | 1343.70 ± 1.17 | 1391.49 ± 1.14 | -3.43% | 45.47 ± 0.02 | 44.76 ± 0.06 | +1.59% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
