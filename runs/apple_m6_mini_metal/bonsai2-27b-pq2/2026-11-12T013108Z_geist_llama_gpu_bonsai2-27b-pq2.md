# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `48a84627b0c5`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.48 ± 0.60 | 235.18 ± 0.45 | +9.06% | 18.94 ± 0.01 | 16.02 ± 0.01 | +18.19% |
| 256 | 259.71 ± 0.15 | 236.58 ± 0.18 | +9.78% | 18.89 ± 0.01 | 16.00 ± 0.01 | +18.04% |
| 512 | 224.65 ± 0.12 | 233.89 ± 0.21 | -3.95% | 18.85 ± 0.01 | 15.93 ± 0.01 | +18.33% |
| 1024 | 222.14 ± 0.05 | 232.56 ± 0.08 | -4.48% | 18.72 ± 0.01 | 15.86 ± 0.01 | +18.05% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
