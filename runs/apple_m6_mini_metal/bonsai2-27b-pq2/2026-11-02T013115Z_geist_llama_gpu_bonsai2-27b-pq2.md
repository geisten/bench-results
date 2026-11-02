# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `e64ff1027649`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.63 ± 0.31 | 235.18 ± 0.14 | +9.12% | 19.02 ± 0.01 | 16.18 ± 0.01 | +17.56% |
| 256 | 259.84 ± 0.43 | 236.77 ± 0.18 | +9.75% | 18.99 ± 0.01 | 16.17 ± 0.01 | +17.46% |
| 512 | 224.79 ± 0.09 | 234.17 ± 0.29 | -4.01% | 18.93 ± 0.02 | 16.09 ± 0.00 | +17.62% |
| 1024 | 222.26 ± 0.12 | 232.34 ± 0.07 | -4.34% | 18.80 ± 0.01 | 16.03 ± 0.00 | +17.29% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
