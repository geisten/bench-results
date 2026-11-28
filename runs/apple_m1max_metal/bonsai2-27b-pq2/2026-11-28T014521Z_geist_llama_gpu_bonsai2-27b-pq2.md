# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `0b0ee998e552`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m1max_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M1 Max, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 160.88 ± 0.12 | 141.89 ± 0.03 | +13.38% | 21.64 ± 0.06 | 21.14 ± 0.03 | +2.36% |
| 256 | 166.07 ± 0.11 | 147.51 ± 0.13 | +12.58% | 21.61 ± 0.06 | 21.07 ± 0.05 | +2.59% |
| 512 | 162.28 ± 0.06 | 126.16 ± 9.82 | +28.63% | 21.44 ± 0.14 | 19.35 ± 1.75 | +10.82% |
| 1024 | 161.69 ± 0.04 | 117.36 ± 1.28 | +37.77% | 21.33 ± 0.05 | 17.44 ± 0.13 | +22.27% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
