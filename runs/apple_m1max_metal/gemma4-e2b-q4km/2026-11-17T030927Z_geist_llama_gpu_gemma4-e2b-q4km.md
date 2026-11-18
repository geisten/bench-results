# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `34c5eb6eb9c9`; llama.cpp `d81235049384`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1390.52 ± 0.66 | 1404.29 ± 1.73 | -0.98% | 119.40 ± 0.17 | 99.73 ± 0.25 | +19.73% |
| 256 | 1562.18 ± 1.48 | 1524.35 ± 1.04 | +2.48% | 118.39 ± 0.09 | 99.96 ± 0.16 | +18.44% |
| 512 | 1561.67 ± 0.61 | 1550.59 ± 0.98 | +0.71% | 117.51 ± 0.83 | 99.75 ± 0.35 | +17.80% |
| 1024 | 1547.47 ± 0.56 | 1485.97 ± 1.09 | +4.14% | 115.44 ± 0.47 | 97.06 ± 0.35 | +18.94% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
