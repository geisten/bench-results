# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `7765ee2a075d`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1274.57 ± 2.86 | 1302.04 ± 1.84 | -2.11% | 45.38 ± 0.02 | 44.74 ± 0.06 | +1.44% |
| 256 | 1335.51 ± 2.90 | 1411.89 ± 0.73 | -5.41% | 45.26 ± 0.01 | 44.47 ± 0.12 | +1.77% |
| 512 | 1333.76 ± 3.41 | 1394.99 ± 0.82 | -4.39% | 44.90 ± 0.00 | 44.41 ± 0.02 | +1.11% |
| 1024 | 1322.95 ± 1.81 | 1381.69 ± 2.51 | -4.25% | 44.70 ± 0.02 | 44.09 ± 0.05 | +1.38% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
