# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 400.01 ± 3.82 | 269.98 ± 1.09 | +48.16% | 25.82 ± 0.04 | 23.08 ± 0.03 | +11.88% |
| 256 | 401.27 ± 1.89 | 273.72 ± 0.63 | +46.60% | 25.78 ± 0.07 | 23.02 ± 0.03 | +11.97% |
| 512 | 403.16 ± 0.99 | 270.45 ± 3.41 | +49.07% | 25.75 ± 0.04 | 23.11 ± 0.14 | +11.40% |
| 1024 | 402.82 ± 1.14 | 272.79 ± 5.16 | +47.67% | 25.62 ± 0.04 | 22.86 ± 0.16 | +12.06% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
