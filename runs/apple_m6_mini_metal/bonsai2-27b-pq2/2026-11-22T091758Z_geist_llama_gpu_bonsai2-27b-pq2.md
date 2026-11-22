# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `7765ee2a075d`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.36 ± 0.18 | 234.95 ± 0.26 | +9.11% | 18.92 ± 0.01 | 16.11 ± 0.01 | +17.42% |
| 256 | 259.00 ± 0.21 | 236.37 ± 0.43 | +9.57% | 18.88 ± 0.00 | 16.09 ± 0.01 | +17.35% |
| 512 | 224.19 ± 0.11 | 233.35 ± 0.27 | -3.93% | 18.83 ± 0.00 | 16.02 ± 0.00 | +17.58% |
| 1024 | 221.56 ± 0.07 | 231.92 ± 0.22 | -4.47% | 18.70 ± 0.00 | 15.95 ± 0.01 | +17.26% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
