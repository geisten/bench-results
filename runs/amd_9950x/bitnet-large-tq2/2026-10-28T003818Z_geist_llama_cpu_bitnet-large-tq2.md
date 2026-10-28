# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `13921becb240`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2603.93 ± 23.99 | 1366.72 ± 6.34 | +90.52% | 324.37 ± 0.74 | 235.02 ± 3.27 | +38.02% |
| 256 | 2572.63 ± 29.68 | 1418.26 ± 4.52 | +81.39% | 305.87 ± 0.41 | 213.73 ± 2.38 | +43.11% |
| 512 | 2358.76 ± 15.58 | 1395.11 ± 1.03 | +69.07% | 274.03 ± 2.42 | 186.14 ± 1.75 | +47.22% |
| 1024 | 2117.06 ± 5.31 | 1333.35 ± 1.78 | +58.78% | 216.86 ± 3.16 | 145.13 ± 1.07 | +49.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
