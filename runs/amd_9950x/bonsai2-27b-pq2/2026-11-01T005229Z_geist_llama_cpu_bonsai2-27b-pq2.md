# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `6642260d55a1`; llama.cpp `adfffbe41b2c`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 84.12 ± 0.57 | 54.39 ± 0.16 | +54.67% | 9.60 ± 0.02 | 8.44 ± 0.02 | +13.85% |
| 256 | 83.40 ± 0.53 | 54.56 ± 0.20 | +52.86% | 9.57 ± 0.02 | 8.40 ± 0.02 | +14.00% |
| 512 | 83.35 ± 0.42 | 53.35 ± 0.18 | +56.22% | 9.56 ± 0.01 | 8.36 ± 0.01 | +14.34% |
| 1024 | 82.81 ± 0.37 | 53.38 ± 0.13 | +55.12% | 9.53 ± 0.01 | 8.34 ± 0.04 | +14.21% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
