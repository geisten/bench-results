# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `a4d332c604a2`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.41 ± 0.16 | 235.75 ± 0.33 | +8.76% | 18.81 ± 0.01 | 15.76 ± 0.01 | +19.36% |
| 256 | 260.18 ± 0.13 | 236.88 ± 0.25 | +9.84% | 18.79 ± 0.01 | 15.75 ± 0.01 | +19.36% |
| 512 | 224.71 ± 0.04 | 233.97 ± 0.32 | -3.96% | 18.73 ± 0.02 | 15.67 ± 0.00 | +19.52% |
| 1024 | 222.16 ± 0.08 | 232.72 ± 0.20 | -4.54% | 18.61 ± 0.02 | 15.60 ± 0.02 | +19.31% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
