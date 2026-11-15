# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `9287d0c3734e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2633.94 ± 5.18 | 2279.20 ± 3.71 | +15.56% | 89.30 ± 0.04 | 85.57 ± 0.10 | +4.36% |
| 256 | 2723.35 ± 4.52 | 2881.41 ± 3.30 | -5.49% | 89.00 ± 0.04 | 85.27 ± 0.10 | +4.38% |
| 512 | 2705.80 ± 1.79 | 2828.89 ± 1.67 | -4.35% | 88.24 ± 0.04 | 84.87 ± 0.14 | +3.97% |
| 1024 | 2655.80 ± 2.10 | 2783.31 ± 2.79 | -4.58% | 87.77 ± 0.01 | 84.03 ± 0.08 | +4.45% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
