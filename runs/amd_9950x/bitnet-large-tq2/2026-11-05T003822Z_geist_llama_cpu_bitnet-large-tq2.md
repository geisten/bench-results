# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `406a3c0519ec`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2600.18 ± 25.95 | 1362.72 ± 4.25 | +90.81% | 322.78 ± 0.76 | 243.38 ± 3.71 | +32.63% |
| 256 | 2558.60 ± 27.83 | 1423.75 ± 4.68 | +79.71% | 304.84 ± 1.10 | 216.26 ± 2.32 | +40.96% |
| 512 | 2367.01 ± 9.69 | 1394.55 ± 6.07 | +69.73% | 272.11 ± 0.65 | 184.84 ± 3.52 | +47.21% |
| 1024 | 2109.92 ± 13.19 | 1336.68 ± 4.28 | +57.85% | 213.33 ± 1.50 | 146.20 ± 0.65 | +45.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
