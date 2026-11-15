# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `9287d0c3734e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1285.19 ± 2.71 | 1311.45 ± 2.11 | -2.00% | 45.73 ± 0.01 | 45.03 ± 0.06 | +1.54% |
| 256 | 1344.85 ± 3.11 | 1418.06 ± 1.76 | -5.16% | 45.59 ± 0.02 | 44.83 ± 0.04 | +1.68% |
| 512 | 1342.84 ± 2.54 | 1402.99 ± 2.02 | -4.29% | 45.25 ± 0.01 | 44.65 ± 0.03 | +1.33% |
| 1024 | 1330.07 ± 1.97 | 1388.22 ± 1.49 | -4.19% | 45.05 ± 0.01 | 44.34 ± 0.05 | +1.59% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
