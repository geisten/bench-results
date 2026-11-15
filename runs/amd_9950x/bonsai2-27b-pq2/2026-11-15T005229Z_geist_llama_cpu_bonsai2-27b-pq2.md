# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `7765b16fc97f`; llama.cpp `adfffbe41b2c`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 83.41 ± 0.75 | 54.30 ± 0.12 | +53.60% | 9.60 ± 0.04 | 8.41 ± 0.01 | +14.09% |
| 256 | 83.50 ± 1.06 | 54.51 ± 0.10 | +53.19% | 9.56 ± 0.03 | 8.36 ± 0.01 | +14.30% |
| 512 | 82.71 ± 0.99 | 54.00 ± 0.05 | +53.16% | 9.53 ± 0.02 | 8.35 ± 0.01 | +14.14% |
| 1024 | 82.54 ± 0.49 | 53.67 ± 0.10 | +53.80% | 9.52 ± 0.01 | 8.30 ± 0.01 | +14.62% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
