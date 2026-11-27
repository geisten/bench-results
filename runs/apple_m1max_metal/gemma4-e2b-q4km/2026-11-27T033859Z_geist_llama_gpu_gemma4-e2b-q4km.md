# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 3430.67 ± 5.71 | 1404.64 ± 2.51 | +144.24% | 122.73 ± 0.34 | 98.57 ± 0.37 | +24.51% |
| 256 | 4241.18 ± 16.72 | 1525.62 ± 0.69 | +178.00% | 122.28 ± 0.24 | 98.87 ± 0.20 | +23.67% |
| 512 | 4464.11 ± 6.71 | 1550.51 ± 1.12 | +187.91% | 121.39 ± 0.12 | 98.59 ± 0.39 | +23.13% |
| 1024 | 4555.85 ± 2.72 | 1486.12 ± 1.08 | +206.56% | 119.12 ± 0.30 | 95.64 ± 0.72 | +24.55% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
