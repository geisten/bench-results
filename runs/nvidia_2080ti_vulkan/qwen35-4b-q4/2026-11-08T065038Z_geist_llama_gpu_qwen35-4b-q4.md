# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1989.71 ± 2.32 | 2681.00 ± 5.24 | -25.78% | 122.73 ± 0.04 | 125.16 ± 0.31 | -1.94% |
| 256 | 2991.88 ± 2.12 | 3369.35 ± 10.85 | -11.20% | 122.44 ± 0.08 | 124.92 ± 0.26 | -1.98% |
| 512 | 3497.57 ± 2.74 | 3360.12 ± 9.67 | +4.09% | 122.07 ± 0.07 | 124.29 ± 0.22 | -1.78% |
| 1024 | 3461.06 ± 5.66 | 3316.49 ± 8.37 | +4.36% | 121.18 ± 0.14 | 122.22 ± 0.31 | -0.85% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
