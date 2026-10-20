# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `44479afd263d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1761.06 ± 40.11 | 1346.12 ± 5.60 | +30.83% | 320.54 ± 1.90 | 232.34 ± 0.96 | +37.96% |
| 256 | 1729.95 ± 17.39 | 1356.09 ± 6.14 | +27.57% | 305.00 ± 1.11 | 207.91 ± 2.40 | +46.69% |
| 512 | 1675.60 ± 22.90 | 1313.09 ± 16.70 | +27.61% | 272.14 ± 3.15 | 181.43 ± 1.88 | +49.99% |
| 1024 | 1542.00 ± 8.46 | 1262.90 ± 9.07 | +22.10% | 218.89 ± 2.61 | 142.90 ± 1.12 | +53.18% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
