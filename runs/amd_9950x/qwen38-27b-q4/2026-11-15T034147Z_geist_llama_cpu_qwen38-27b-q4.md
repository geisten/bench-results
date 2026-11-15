# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 98.23 ± 6.65 | 55.62 ± 0.14 | +76.61% | 4.86 ± 0.03 | 4.49 ± 0.01 | +8.27% |
| 256 | 96.67 ± 3.97 | 56.11 ± 0.10 | +72.28% | 4.86 ± 0.01 | 4.48 ± 0.01 | +8.43% |
| 512 | 96.73 ± 4.21 | 55.36 ± 0.52 | +74.73% | 4.85 ± 0.01 | 4.48 ± 0.01 | +8.32% |
| 1024 | 96.15 ± 1.35 | 55.44 ± 0.45 | +73.44% | 4.84 ± 0.01 | 4.45 ± 0.01 | +8.67% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
