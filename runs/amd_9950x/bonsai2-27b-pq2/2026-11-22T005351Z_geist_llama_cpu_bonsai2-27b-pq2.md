# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `aeb3a50153d7`; llama.cpp `adfffbe41b2c`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 82.87 ± 0.76 | 53.35 ± 0.26 | +55.34% | 9.53 ± 0.04 | 8.42 ± 0.01 | +13.16% |
| 256 | 81.49 ± 0.99 | 53.57 ± 0.23 | +52.12% | 9.50 ± 0.04 | 8.37 ± 0.01 | +13.50% |
| 512 | 81.60 ± 0.71 | 52.31 ± 0.35 | +55.99% | 9.48 ± 0.03 | 8.36 ± 0.01 | +13.52% |
| 1024 | 81.07 ± 0.81 | 52.48 ± 0.30 | +54.47% | 9.44 ± 0.05 | 8.33 ± 0.02 | +13.33% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
