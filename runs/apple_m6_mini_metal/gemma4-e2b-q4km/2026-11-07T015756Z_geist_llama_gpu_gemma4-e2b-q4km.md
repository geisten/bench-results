# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2629.44 ± 3.22 | 2284.74 ± 3.57 | +15.09% | 90.17 ± 0.03 | 86.27 ± 0.07 | +4.52% |
| 256 | 2718.94 ± 3.67 | 2881.47 ± 2.84 | -5.64% | 89.83 ± 0.04 | 86.12 ± 0.14 | +4.31% |
| 512 | 2700.32 ± 2.27 | 2827.45 ± 1.91 | -4.50% | 89.13 ± 0.02 | 85.55 ± 0.13 | +4.19% |
| 1024 | 2651.62 ± 0.99 | 2781.99 ± 2.63 | -4.69% | 88.58 ± 0.03 | 84.76 ± 0.20 | +4.50% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
