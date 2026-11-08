# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `ff31d42364e1`; llama.cpp `adfffbe41b2c`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 83.40 ± 1.23 | 54.25 ± 0.12 | +53.72% | 9.61 ± 0.03 | 8.36 ± 0.01 | +14.90% |
| 256 | 83.02 ± 0.94 | 54.49 ± 0.09 | +52.35% | 9.59 ± 0.02 | 8.30 ± 0.01 | +15.50% |
| 512 | 82.93 ± 0.90 | 53.91 ± 0.06 | +53.82% | 9.59 ± 0.02 | 8.30 ± 0.01 | +15.56% |
| 1024 | 82.58 ± 0.74 | 53.47 ± 0.15 | +54.45% | 9.54 ± 0.02 | 8.23 ± 0.01 | +15.91% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
