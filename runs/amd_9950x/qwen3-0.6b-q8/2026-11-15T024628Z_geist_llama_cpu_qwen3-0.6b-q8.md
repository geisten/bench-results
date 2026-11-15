# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2096.94 ± 27.99 | 1630.87 ± 4.65 | +28.58% | 117.47 ± 0.93 | 107.31 ± 0.28 | +9.46% |
| 256 | 2085.97 ± 21.84 | 1666.46 ± 6.63 | +25.17% | 115.19 ± 0.25 | 109.20 ± 0.90 | +5.48% |
| 512 | 2011.08 ± 10.22 | 1672.51 ± 2.57 | +20.24% | 112.01 ± 0.40 | 103.94 ± 0.63 | +7.76% |
| 1024 | 1909.55 ± 4.77 | 1540.53 ± 5.43 | +23.95% | 105.71 ± 0.35 | 94.73 ± 0.70 | +11.59% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
