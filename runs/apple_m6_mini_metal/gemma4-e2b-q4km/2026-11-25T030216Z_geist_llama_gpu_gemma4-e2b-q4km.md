# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5219.27 ± 10.02 | 2275.16 ± 4.06 | +129.40% | 89.50 ± 0.07 | 85.21 ± 0.10 | +5.04% |
| 256 | 6935.89 ± 20.82 | 2881.71 ± 4.22 | +140.69% | 89.28 ± 0.04 | 84.90 ± 0.15 | +5.16% |
| 512 | 7677.03 ± 5.64 | 2826.82 ± 2.63 | +171.58% | 88.52 ± 0.05 | 84.43 ± 0.22 | +4.84% |
| 1024 | 7948.37 ± 5.99 | 2774.64 ± 1.47 | +186.46% | 88.02 ± 0.07 | 83.73 ± 0.14 | +5.13% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
