# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `d46135a24bb6`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1376.66 ± 2.68 | 1367.95 ± 2.59 | +0.64% | 49.14 ± 0.04 | 49.14 ± 0.02 | -0.00% |
| 256 | 1513.99 ± 1.96 | 1461.64 ± 1.27 | +3.58% | 49.08 ± 0.02 | 48.95 ± 0.02 | +0.27% |
| 512 | 1526.60 ± 0.65 | 1429.45 ± 12.57 | +6.80% | 48.90 ± 0.01 | 48.71 ± 0.01 | +0.40% |
| 1024 | 1522.27 ± 1.47 | 1422.00 ± 2.33 | +7.05% | 48.55 ± 0.02 | 48.43 ± 0.02 | +0.24% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
