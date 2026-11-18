# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `34c5eb6eb9c9`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 158.63 ± 0.10 | 141.96 ± 0.03 | +11.75% | 21.47 ± 0.05 | 21.13 ± 0.05 | +1.60% |
| 256 | 165.78 ± 0.20 | 147.35 ± 0.04 | +12.51% | 21.38 ± 0.03 | 20.94 ± 0.22 | +2.11% |
| 512 | 161.58 ± 0.06 | 131.76 ± 15.66 | +22.63% | 21.26 ± 0.05 | 19.17 ± 1.82 | +10.88% |
| 1024 | 161.33 ± 0.04 | 115.67 ± 1.18 | +39.47% | 21.09 ± 0.06 | 17.27 ± 0.13 | +22.14% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
