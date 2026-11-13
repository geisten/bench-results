# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `0b27a7bb678a`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.89 ± 0.26 | 235.31 ± 0.26 | +9.17% | 18.93 ± 0.00 | 16.00 ± 0.02 | +18.30% |
| 256 | 259.69 ± 0.24 | 236.63 ± 0.35 | +9.74% | 18.89 ± 0.01 | 15.99 ± 0.02 | +18.18% |
| 512 | 224.61 ± 0.03 | 233.75 ± 0.22 | -3.91% | 18.85 ± 0.00 | 15.91 ± 0.02 | +18.44% |
| 1024 | 222.06 ± 0.05 | 232.57 ± 0.29 | -4.52% | 18.71 ± 0.01 | 15.84 ± 0.03 | +18.15% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
