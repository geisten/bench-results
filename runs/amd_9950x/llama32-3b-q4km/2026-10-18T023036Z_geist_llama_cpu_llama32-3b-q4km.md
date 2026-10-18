# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 737.03 ± 2.89 | 496.08 ± 2.04 | +48.57% | 37.38 ± 0.14 | 35.60 ± 0.07 | +5.02% |
| 256 | 741.32 ± 3.80 | 506.95 ± 1.50 | +46.23% | 37.36 ± 0.10 | 35.11 ± 0.04 | +6.40% |
| 512 | 725.13 ± 4.94 | 510.94 ± 1.49 | +41.92% | 37.01 ± 0.06 | 34.46 ± 0.02 | +7.41% |
| 1024 | 702.48 ± 3.73 | 496.72 ± 0.96 | +41.42% | 36.43 ± 0.08 | 33.25 ± 0.06 | +9.56% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
