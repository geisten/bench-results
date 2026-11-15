# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 740.78 ± 1.91 | 499.96 ± 2.06 | +48.17% | 37.54 ± 0.08 | 35.73 ± 0.06 | +5.07% |
| 256 | 743.06 ± 2.63 | 509.29 ± 1.55 | +45.90% | 37.39 ± 0.13 | 35.16 ± 0.07 | +6.34% |
| 512 | 736.79 ± 4.41 | 511.68 ± 0.84 | +43.99% | 37.09 ± 0.13 | 34.54 ± 0.07 | +7.38% |
| 1024 | 706.10 ± 5.10 | 497.60 ± 1.57 | +41.90% | 36.44 ± 0.07 | 33.44 ± 0.03 | +8.96% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
