# CISLR Stage 4.6 — Model Comparison & Scientific Selection

## Selected Model

**MobileNetV3-Large**

## Objective

Stage 4.6 combines the Stage 4.3 computational benchmark and Stage 4.5 official CISLR prototype-to-test retrieval evaluation to select a deployment-oriented candidate for OpenVINO conversion.

## Final Comparison

| Model             |     Top1 |     Top5 |   Recall10 |      MRR |   Mean_Rank |   Median_Rank |   CPU_FPS |   GPU_FPS |   GFLOPs |   Model_Size_MB |   Params |   Peak_GPU_Memory_MB |   Retrieval_Score |   Efficiency_Score |   Overall_Deployment_Score |   Overall_Rank |
|:------------------|---------:|---------:|-----------:|---------:|------------:|--------------:|----------:|----------:|---------:|----------------:|---------:|---------------------:|------------------:|-------------------:|---------------------------:|---------------:|
| MobileNetV3-Large | 0.157987 | 0.237199 |   0.266521 | 0.195284 |     1572.52 |          1229 |   52.6631 |   186.513 | 0.442815 |         39.5006 | 10304716 |              56.6206 |         1         |            0.98425 |                  0.994487  |              1 |
| EfficientNet-B0   | 0.128665 | 0.212254 |   0.243764 | 0.169579 |     1781.71 |          1681 |   29.1245 |   132.23  | 0.781265 |         38.8467 | 10110232 |              59.1011 |         0.192255  |            0.69902 |                  0.369623  |              2 |
| ResNet18          | 0.111597 | 0.213129 |   0.252954 | 0.157626 |     1389.87 |           856 |   16.841  |   418.238 | 3.632    |         52.0313 | 13620444 |              71.2842 |         0.0895412 |            0       |                  0.0582018 |              3 |

## Selection Method

- Retrieval weight: 0.65
- Efficiency weight: 0.35
- Retrieval: Top-1, Top-5, Recall@10 and MRR.
- Efficiency: CPU FPS, GFLOPs, model size, parameter count and peak GPU memory.

## Scientific Decision

Stage 4.6 selects MobileNetV3-Large as the primary deployment candidate for OpenVINO conversion. The selection is based on the joint evaluation of official CISLR prototype-to-test retrieval performance and computational efficiency. MobileNetV3-Large achieved the strongest Top-1, Top-5, Recall@10 and MRR among the evaluated architectures while also providing substantially lower computational cost than ResNet18. ResNet18 remains superior in GPU batch-1 latency and mean/median retrieval rank, so MobileNetV3-Large is not claimed to dominate every metric. Instead, it is selected as the best balanced deployment candidate under the defined criteria. OpenVINO conversion and benchmarking will provide the final deployment validation.

## Caveats

- Stage 4.4 training accuracy is a convergence diagnostic, not the official CISLR evaluation metric.
- Stage 4.5 evaluates prototype-to-test retrieval rather than conventional closed-set classification.
- The official prototype set contains one prototype video per class.
- The Stage 4.4 frozen training pool contained 4,417 readable videos/classes, whereas the valid prototype set contains 4,764 videos.
- Therefore, 347 prototype videos/classes were not represented in the frozen Stage 4.4 training pool.
- Stage 4.5 uses mean penultimate embeddings for cosine retrieval rather than classifier logits.
- ResNet18 has the fastest GPU batch-1 latency in Stage 4.3 and remains relevant for GPU-only deployment scenarios.
- The Stage 4.6 weighted score is a transparent decision framework for this project and is not a universal model quality metric.
- OpenVINO conversion and benchmarking are required before making final deployment-speed claims.
