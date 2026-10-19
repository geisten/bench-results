# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `2b5263f87833`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1803.54 ± 25.68 | 1335.78 ± 9.81 | +35.02% | 317.68 ± 4.76 | 240.36 ± 3.17 | +32.17% |
| 256 | 1741.14 ± 22.53 | 1360.83 ± 2.70 | +27.95% | 302.05 ± 2.23 | 198.94 ± 3.41 | +51.82% |
| 512 | 1692.18 ± 34.12 | 1334.10 ± 6.05 | +26.84% | 269.90 ± 3.05 | 170.41 ± 2.70 | +58.38% |
| 1024 | 1582.65 ± 12.87 | 1278.05 ± 3.78 | +23.83% | 213.27 ± 3.78 | 132.18 ± 2.06 | +61.35% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
