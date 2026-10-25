# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `af6689407a1d`; llama.cpp `adfffbe41b2c`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 83.53 ± 0.66 | 53.63 ± 0.13 | +55.75% | 9.57 ± 0.03 | 8.43 ± 0.01 | +13.46% |
| 256 | 83.65 ± 0.17 | 53.90 ± 0.14 | +55.18% | 9.57 ± 0.02 | 8.37 ± 0.01 | +14.35% |
| 512 | 83.37 ± 0.21 | 52.85 ± 0.14 | +57.74% | 9.55 ± 0.03 | 8.37 ± 0.02 | +14.07% |
| 1024 | 82.95 ± 0.20 | 52.57 ± 0.09 | +57.78% | 9.53 ± 0.03 | 8.33 ± 0.03 | +14.43% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
