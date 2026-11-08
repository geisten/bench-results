# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1274.41 ± 1.05 | 1306.47 ± 1.29 | -2.45% | 45.26 ± 0.01 | 44.41 ± 0.03 | +1.92% |
| 256 | 1354.55 ± 1.73 | 1417.17 ± 1.63 | -4.42% | 45.13 ± 0.01 | 44.21 ± 0.03 | +2.07% |
| 512 | 1353.19 ± 0.50 | 1402.26 ± 1.22 | -3.50% | 44.78 ± 0.02 | 44.02 ± 0.05 | +1.71% |
| 1024 | 1339.55 ± 0.80 | 1389.19 ± 1.39 | -3.57% | 44.58 ± 0.03 | 43.70 ± 0.05 | +2.01% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
