# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `7765b16fc97f`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 257.04 ± 0.37 | 236.12 ± 0.25 | +8.86% | 19.14 ± 0.00 | 16.38 ± 0.01 | +16.83% |
| 256 | 260.40 ± 0.32 | 237.67 ± 0.23 | +9.56% | 19.10 ± 0.01 | 16.37 ± 0.01 | +16.69% |
| 512 | 225.22 ± 0.09 | 235.48 ± 0.22 | -4.36% | 19.05 ± 0.01 | 16.29 ± 0.01 | +16.97% |
| 1024 | 222.63 ± 0.06 | 233.47 ± 0.14 | -4.64% | 18.92 ± 0.00 | 16.22 ± 0.01 | +16.66% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
