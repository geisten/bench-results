# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2541.83 ± 43.51 | 1360.33 ± 3.27 | +86.85% | 321.48 ± 5.87 | 230.60 ± 7.80 | +39.41% |
| 256 | 2488.63 ± 36.75 | 1394.26 ± 9.36 | +78.49% | 304.25 ± 2.52 | 196.18 ± 8.88 | +55.08% |
| 512 | 2323.18 ± 32.58 | 1367.57 ± 2.44 | +69.88% | 269.19 ± 3.39 | 168.43 ± 2.07 | +59.82% |
| 1024 | 2068.19 ± 23.64 | 1322.95 ± 2.10 | +56.33% | 215.04 ± 3.61 | 126.64 ± 1.01 | +69.81% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
