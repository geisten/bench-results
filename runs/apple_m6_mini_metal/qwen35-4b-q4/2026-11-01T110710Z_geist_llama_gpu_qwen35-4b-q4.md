# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1383.75 ± 3.61 | 1375.61 ± 1.83 | +0.59% | 49.64 ± 0.02 | 49.83 ± 0.02 | -0.38% |
| 256 | 1519.15 ± 1.56 | 1466.99 ± 0.98 | +3.56% | 49.56 ± 0.02 | 49.43 ± 0.05 | +0.25% |
| 512 | 1533.42 ± 0.59 | 1425.94 ± 5.52 | +7.54% | 49.40 ± 0.01 | 49.20 ± 0.04 | +0.42% |
| 1024 | 1529.07 ± 0.41 | 1426.18 ± 3.52 | +7.21% | 49.02 ± 0.02 | 48.99 ± 0.03 | +0.07% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
