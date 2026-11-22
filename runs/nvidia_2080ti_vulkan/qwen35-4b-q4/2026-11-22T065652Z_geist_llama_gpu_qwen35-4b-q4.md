# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1996.19 ± 8.59 | 2683.09 ± 4.20 | -25.60% | 131.71 ± 0.13 | 124.41 ± 0.20 | +5.87% |
| 256 | 3004.01 ± 2.36 | 3372.23 ± 6.72 | -10.92% | 131.53 ± 0.08 | 124.69 ± 0.50 | +5.48% |
| 512 | 3506.57 ± 4.69 | 3354.96 ± 3.17 | +4.52% | 131.36 ± 0.21 | 123.95 ± 0.61 | +5.98% |
| 1024 | 3466.77 ± 4.13 | 3322.26 ± 7.57 | +4.35% | 130.48 ± 0.27 | 122.45 ± 0.54 | +6.55% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
