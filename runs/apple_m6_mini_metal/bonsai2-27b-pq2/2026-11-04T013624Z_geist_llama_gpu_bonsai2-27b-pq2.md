# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `13cb783eddd2`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.99 ± 0.31 | 236.04 ± 0.27 | +8.88% | 19.18 ± 0.02 | 16.60 ± 0.01 | +15.58% |
| 256 | 260.15 ± 0.27 | 237.76 ± 0.35 | +9.42% | 19.14 ± 0.03 | 16.57 ± 0.01 | +15.47% |
| 512 | 225.07 ± 0.11 | 235.13 ± 0.26 | -4.28% | 19.10 ± 0.01 | 16.49 ± 0.01 | +15.82% |
| 1024 | 222.57 ± 0.05 | 233.52 ± 0.29 | -4.69% | 18.96 ± 0.01 | 16.41 ± 0.02 | +15.52% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
