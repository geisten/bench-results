# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `c993379b0746`; llama.cpp `adfffbe41b2c`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 52.94 ± 0.27 | 53.99 ± 0.18 | -1.93% | 9.57 ± 0.04 | 8.37 ± 0.01 | +14.36% |
| 256 | 52.83 ± 0.12 | 54.18 ± 0.10 | -2.50% | 9.56 ± 0.04 | 8.32 ± 0.01 | +14.87% |
| 512 | 52.67 ± 0.06 | 53.67 ± 0.11 | -1.86% | 9.47 ± 0.04 | 8.28 ± 0.03 | +14.37% |
| 1024 | 52.54 ± 0.09 | 53.44 ± 0.10 | -1.67% | 9.45 ± 0.04 | 8.24 ± 0.01 | +14.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
