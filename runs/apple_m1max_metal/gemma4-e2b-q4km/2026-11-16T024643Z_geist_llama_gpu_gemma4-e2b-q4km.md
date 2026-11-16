# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `199d6ecb49dd`; llama.cpp `d81235049384`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1394.05 ± 2.56 | 1405.63 ± 1.30 | -0.82% | 119.91 ± 0.47 | 99.97 ± 0.32 | +19.95% |
| 256 | 1564.76 ± 2.97 | 1524.64 ± 1.08 | +2.63% | 119.13 ± 0.56 | 100.12 ± 0.14 | +18.98% |
| 512 | 1562.40 ± 1.61 | 1550.41 ± 0.84 | +0.77% | 117.53 ± 0.32 | 99.96 ± 0.14 | +17.57% |
| 1024 | 1547.70 ± 0.86 | 1486.22 ± 1.33 | +4.14% | 115.69 ± 0.43 | 96.58 ± 0.33 | +19.78% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
