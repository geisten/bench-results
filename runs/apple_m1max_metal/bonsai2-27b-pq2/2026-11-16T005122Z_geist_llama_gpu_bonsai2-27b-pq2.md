# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `99e847f1c898`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 158.62 ± 0.46 | 141.97 ± 0.05 | +11.73% | 21.41 ± 0.03 | 21.11 ± 0.02 | +1.45% |
| 256 | 165.89 ± 0.26 | 147.33 ± 0.35 | +12.60% | 21.39 ± 0.04 | 21.02 ± 0.12 | +1.75% |
| 512 | 161.75 ± 0.08 | 128.33 ± 11.34 | +26.04% | 21.28 ± 0.19 | 18.15 ± 1.07 | +17.29% |
| 1024 | 161.38 ± 0.05 | 117.44 ± 1.18 | +37.42% | 21.10 ± 0.15 | 17.16 ± 0.26 | +22.92% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
