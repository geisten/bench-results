# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `4afb05f241a0`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on AMD Ryzen 9 9950X 16-Core Processor (RADV RAPHAEL_MENDOCINO), same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 14.48 ± 0.05 | 48.60 ± 0.19 | -70.21% | 6.52 ± 0.00 | 8.09 ± 0.00 | -19.46% |
| 256 | 13.92 ± 0.05 | 48.96 ± 0.06 | -71.57% | 6.67 ± 0.00 | 7.97 ± 0.00 | -16.34% |
| 512 | 12.80 ± 0.04 | 48.61 ± 0.10 | -73.67% | 6.57 ± 0.00 | 7.84 ± 0.00 | -16.28% |
| 1024 | 11.62 ± 0.03 | 48.24 ± 0.08 | -75.92% | 6.49 ± 0.00 | 7.79 ± 0.00 | -16.68% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
