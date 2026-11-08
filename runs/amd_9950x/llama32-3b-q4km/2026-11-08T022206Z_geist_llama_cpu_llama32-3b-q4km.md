# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 739.71 ± 1.97 | 504.76 ± 4.34 | +46.55% | 37.51 ± 0.08 | 35.56 ± 0.04 | +5.48% |
| 256 | 743.46 ± 5.46 | 516.12 ± 2.39 | +44.05% | 37.31 ± 0.03 | 35.08 ± 0.06 | +6.37% |
| 512 | 736.48 ± 4.23 | 520.36 ± 1.25 | +41.53% | 36.98 ± 0.07 | 34.38 ± 0.04 | +7.56% |
| 1024 | 698.52 ± 6.73 | 502.68 ± 2.81 | +38.96% | 36.40 ± 0.05 | 33.24 ± 0.06 | +9.49% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
