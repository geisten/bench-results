# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `7458b37b9531`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 741.01 ± 1.45 | 503.05 ± 3.18 | +47.30% | 37.55 ± 0.09 | 35.66 ± 0.04 | +5.29% |
| 256 | 745.21 ± 1.91 | 514.94 ± 1.03 | +44.72% | 37.38 ± 0.09 | 35.14 ± 0.01 | +6.39% |
| 512 | 736.42 ± 6.18 | 520.03 ± 1.16 | +41.61% | 37.03 ± 0.04 | 34.54 ± 0.02 | +7.22% |
| 1024 | 709.89 ± 4.50 | 503.30 ± 0.65 | +41.05% | 36.44 ± 0.08 | 33.30 ± 0.07 | +9.45% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
