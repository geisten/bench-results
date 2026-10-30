# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `50863de30fe7`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 93.31 ± 0.01 | 234.97 ± 0.05 | -60.29% | 18.95 ± 0.01 | 16.16 ± 0.01 | +17.30% |
| 256 | 95.77 ± 0.01 | 236.80 ± 0.17 | -59.55% | 18.92 ± 0.01 | 16.11 ± 0.03 | +17.46% |
| 512 | 95.85 ± 0.01 | 233.87 ± 0.21 | -59.01% | 18.86 ± 0.01 | 15.97 ± 0.11 | +18.09% |
| 1024 | 95.20 ± 0.01 | 232.30 ± 0.11 | -59.02% | 18.71 ± 0.02 | 15.77 ± 0.11 | +18.66% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
