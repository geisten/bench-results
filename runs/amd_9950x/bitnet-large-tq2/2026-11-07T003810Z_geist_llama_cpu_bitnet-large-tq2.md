# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1854.12 ± 11.57 | 1343.52 ± 4.44 | +38.00% | 324.27 ± 2.26 | 240.52 ± 2.22 | +34.82% |
| 256 | 1802.46 ± 26.73 | 1361.65 ± 1.40 | +32.37% | 308.06 ± 0.77 | 209.95 ± 4.90 | +46.73% |
| 512 | 1760.32 ± 15.61 | 1340.99 ± 11.86 | +31.27% | 277.08 ± 2.26 | 178.58 ± 4.81 | +55.15% |
| 1024 | 1616.31 ± 25.08 | 1280.66 ± 23.67 | +26.21% | 221.69 ± 4.68 | 141.41 ± 1.97 | +56.77% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
