# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 501.26 ± 3.10 | 322.06 ± 1.13 | +55.64% | 26.19 ± 0.03 | 22.97 ± 0.04 | +14.02% |
| 256 | 493.74 ± 9.64 | 328.08 ± 1.09 | +50.49% | 26.14 ± 0.03 | 22.78 ± 0.05 | +14.73% |
| 512 | 495.60 ± 6.28 | 335.92 ± 0.94 | +47.54% | 26.02 ± 0.03 | 22.54 ± 0.02 | +15.44% |
| 1024 | 490.63 ± 4.61 | 329.09 ± 2.21 | +49.09% | 25.93 ± 0.05 | 22.38 ± 0.04 | +15.87% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
