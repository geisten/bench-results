# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `e64ff1027649`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2651.97 ± 8.57 | 2283.41 ± 3.04 | +16.14% | 90.91 ± 0.02 | 88.14 ± 0.12 | +3.14% |
| 256 | 2766.04 ± 4.76 | 2882.99 ± 1.91 | -4.06% | 90.65 ± 0.02 | 87.71 ± 0.20 | +3.35% |
| 512 | 2745.11 ± 3.82 | 2824.11 ± 1.86 | -2.80% | 89.92 ± 0.01 | 87.24 ± 0.23 | +3.07% |
| 1024 | 2694.83 ± 2.89 | 2775.81 ± 1.05 | -2.92% | 89.39 ± 0.03 | 86.45 ± 0.22 | +3.40% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
