# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1821.12 ± 55.24 | 1208.69 ± 55.41 | +50.67% | 299.87 ± 6.12 | 223.64 ± 2.69 | +34.09% |
| 256 | 1791.81 ± 25.68 | 1234.42 ± 31.35 | +45.15% | 284.70 ± 4.55 | 203.05 ± 4.36 | +40.21% |
| 512 | 1697.53 ± 14.40 | 1211.85 ± 31.42 | +40.08% | 254.65 ± 3.12 | 170.98 ± 7.62 | +48.94% |
| 1024 | 1577.70 ± 15.61 | 1199.97 ± 12.41 | +31.48% | 206.23 ± 2.24 | 134.83 ± 2.73 | +52.96% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
