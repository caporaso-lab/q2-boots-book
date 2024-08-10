# (A) `resample` `Pipeline`
```mermaid
flowchart TD

    feature-table["FeatureTable"] --> resample
    n(["n (Int)"]) --> resample
    sampling-depth(["sampling-depth (Int)"]) --> resample
    replacement(["replacement (Bool)"]) --> resample
    resample{qiime feature-table resample} -->
    feature-collection["Collection[FeatureTable]"]
```

# (B) `alpha` `Pipeline`

```mermaid
flowchart TD

    feature-table["FeatureTable"] --> alpha-collection
    phylogeny["Phylogeny[Rooted]"] -- optional --> alpha-collection
    n(["n (Int)"]) --> alpha-collection
    sampling-depth(["sampling-depth (Int)"]) --> alpha-collection
    replacement(["replacement (Bool)"]) --> alpha-collection
    alpha-metric(["metric (30 choices)"]) --> alpha-collection
    alpha-collection{qiime diversity alpha-collection} --> sd-collection
    average-method(["average method (Choice: median, mean)"]) --> alpha-average
    sd-collection["Collection[SampleData[AlphaDiversity]]"] -->
    alpha-average{qiime boots alpha-average} -->
    sample-data["SampleData[AlphaDiversity]"]
```


# (C) `beta` `Pipeline`

```mermaid
flowchart TD

    feature-table["FeatureTable"] --> beta-collection
    phylogeny["Phylogeny[Rooted]"] -- optional --> beta-collection
    n(["n (Int)"]) --> beta-collection
    sampling-depth(["sampling-depth (Int)"]) --> beta-collection
    replacement(["replacement (Bool)"]) --> beta-collection
    beta-metric(["metric (22 choices)"]) --> beta-collection
    beta-collection{qiime diversity beta-collection} --> dm-collection
    average-method(["average method (Choice: medoid, non-metric-mean, non-metric-median)"]) --> beta-average
    dm-collection[["DistanceMatrix"]] --> beta-average
    beta-average{qiime boots beta-average} -->
    distance-matrix["DistanceMatrix"]
```

```mermaid
flowchart LR
    function-call{QIIME 2 `Action`}
    QIIME 2 `Artifact`
    parameter([parameter])

    style Beta fill:#CC6677
    style Alpha fill:#88CCEE
    AB[Alpha and Beta]
    style AB fill:#DDCC77
    core-metrics[Core Metrics]
    style core-metrics fill:white
```