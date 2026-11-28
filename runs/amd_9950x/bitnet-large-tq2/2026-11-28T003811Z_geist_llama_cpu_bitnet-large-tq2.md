# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `a7a01a052466`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2547.28 ± 70.40 | 1358.80 ± 4.14 | +87.46% | 322.61 ± 2.19 | 238.50 ± 1.71 | +35.27% |
| 256 | 2486.43 ± 42.32 | 1388.70 ± 13.32 | +79.05% | 304.62 ± 1.55 | 209.69 ± 1.41 | +45.27% |
| 512 | 2329.08 ± 19.92 | 1371.72 ± 4.45 | +69.79% | 272.95 ± 0.83 | 181.66 ± 1.92 | +50.25% |
| 1024 | 2074.23 ± 13.35 | 1324.73 ± 3.37 | +56.58% | 212.67 ± 2.30 | 142.17 ± 1.22 | +49.58% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
