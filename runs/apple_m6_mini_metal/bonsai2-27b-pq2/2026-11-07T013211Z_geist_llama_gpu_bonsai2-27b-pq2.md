# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `495156f8079f`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.74 ± 0.25 | 235.42 ± 0.33 | +9.05% | 18.91 ± 0.01 | 15.85 ± 0.02 | +19.31% |
| 256 | 259.97 ± 0.11 | 236.96 ± 0.10 | +9.71% | 18.88 ± 0.00 | 15.84 ± 0.01 | +19.19% |
| 512 | 224.83 ± 0.08 | 234.40 ± 0.45 | -4.08% | 18.84 ± 0.00 | 15.77 ± 0.01 | +19.47% |
| 1024 | 222.26 ± 0.06 | 232.89 ± 0.20 | -4.57% | 18.71 ± 0.00 | 15.59 ± 0.13 | +20.01% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
