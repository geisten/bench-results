# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `527bf29dd426`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2329.39 ± 112.64 | 1354.70 ± 5.40 | +71.95% | 323.68 ± 1.41 | 237.93 ± 1.55 | +36.04% |
| 256 | 2342.89 ± 8.80 | 1410.65 ± 8.54 | +66.08% | 305.45 ± 0.80 | 211.57 ± 2.15 | +44.38% |
| 512 | 2209.21 ± 12.56 | 1379.98 ± 3.74 | +60.09% | 272.69 ± 1.97 | 184.10 ± 0.74 | +48.12% |
| 1024 | 1999.53 ± 6.08 | 1331.60 ± 3.52 | +50.16% | 214.68 ± 2.75 | 144.18 ± 0.88 | +48.89% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
