# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `29a0ce4b5937`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.29 ± 1.94 | 516.03 ± 5.60 | +11.29% | 40.48 ± 0.04 | 28.90 ± 0.05 | +40.09% |
| 256 | 589.37 ± 0.98 | 534.46 ± 4.85 | +10.27% | 40.30 ± 0.06 | 28.92 ± 0.09 | +39.35% |
| 512 | 632.52 ± 1.87 | 543.22 ± 5.16 | +16.44% | 39.94 ± 0.06 | 29.64 ± 0.10 | +34.73% |
| 1024 | 624.08 ± 1.26 | 542.52 ± 5.34 | +15.04% | 39.58 ± 0.09 | 29.29 ± 0.11 | +35.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
