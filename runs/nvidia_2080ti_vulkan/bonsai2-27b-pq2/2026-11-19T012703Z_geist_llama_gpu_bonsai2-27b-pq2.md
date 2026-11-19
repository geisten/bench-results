# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `f261cadcf982`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.25 ± 0.77 | 516.35 ± 4.35 | +11.41% | 40.62 ± 0.04 | 29.22 ± 0.09 | +39.03% |
| 256 | 589.12 ± 2.41 | 535.27 ± 4.67 | +10.06% | 40.40 ± 0.08 | 29.31 ± 0.03 | +37.84% |
| 512 | 632.91 ± 0.93 | 548.75 ± 4.18 | +15.34% | 40.07 ± 0.03 | 29.68 ± 0.07 | +35.00% |
| 1024 | 625.14 ± 1.45 | 540.98 ± 5.31 | +15.56% | 39.71 ± 0.07 | 29.38 ± 0.10 | +35.18% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
