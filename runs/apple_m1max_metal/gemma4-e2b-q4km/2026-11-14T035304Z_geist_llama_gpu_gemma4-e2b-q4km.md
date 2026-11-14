# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1390.44 ± 0.97 | 1404.91 ± 1.46 | -1.03% | 119.17 ± 0.22 | 99.88 ± 0.26 | +19.32% |
| 256 | 1562.50 ± 1.62 | 1524.53 ± 1.08 | +2.49% | 118.65 ± 0.51 | 99.98 ± 0.23 | +18.68% |
| 512 | 1561.24 ± 1.70 | 1550.49 ± 2.55 | +0.69% | 117.44 ± 0.20 | 99.65 ± 0.18 | +17.85% |
| 1024 | 1547.46 ± 0.84 | 1485.72 ± 0.74 | +4.16% | 115.24 ± 0.29 | 96.75 ± 0.36 | +19.11% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
