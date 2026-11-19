# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2567.97 ± 26.05 | 1360.06 ± 2.68 | +88.81% | 321.36 ± 1.55 | 240.66 ± 0.85 | +33.53% |
| 256 | 2530.05 ± 36.02 | 1399.50 ± 10.50 | +80.78% | 305.95 ± 1.19 | 212.89 ± 1.76 | +43.71% |
| 512 | 2360.45 ± 15.60 | 1372.68 ± 3.83 | +71.96% | 272.50 ± 0.74 | 185.08 ± 0.69 | +47.23% |
| 1024 | 2098.27 ± 13.46 | 1326.20 ± 1.57 | +58.22% | 214.71 ± 2.48 | 144.62 ± 1.18 | +48.47% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
