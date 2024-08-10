# Diagram of q2-boots `Pipelines`

## `resample` `Pipeline`
```{mermaid}
flowchart TD

    feature-table["FeatureTable"] --> resample
    n(["n (Int)"]) --> resample
    sampling-depth(["sampling-depth (Int)"]) --> resample
    replacement(["replacement (Bool)"]) --> resample
    resample{"qiime feature-table resample"} --> feature-collection
    feature-collection[["FeatureTable"]]
```

## `alpha` `Pipeline`

```{mermaid}
flowchart TD

    feature-table["FeatureTable"] --> alpha-collection
    phylogeny["Phylogeny[Rooted]"] -- optional --> alpha-collection
    n(["n (Int)"]) --> alpha-collection
    sampling-depth(["sampling-depth (Int)"]) --> alpha-collection
    replacement(["replacement (Bool)"]) --> alpha-collection
    alpha-metric(["metric (30 choices)"]) --> alpha-collection
    alpha-collection{qiime diversity alpha-collection} --> alpha-diversity-collection
    average-method(["average method (Choice: median, mean)"]) --> alpha-average
    alpha-diversity-collection[["SampleData[AlphaDiversity]"]] --> alpha-average
    alpha-average{qiime boots alpha-average} --> alpha-diversity
    alpha-diversity["SampleData[AlphaDiversity]"]
```


# `beta` `Pipeline`

```{mermaid}
flowchart TD

    feature-table["FeatureTable"] --> beta-collection
    phylogeny["Phylogeny[Rooted]"] -- optional --> beta-collection
    n(["n (Int)"]) --> beta-collection
    sampling-depth(["sampling-depth (Int)"]) --> beta-collection
    replacement(["replacement (Bool)"]) --> beta-collection
    beta-metric(["metric (22 choices)"]) --> beta-collection
    beta-collection{qiime diversity beta-collection} --> distance-matrix-collection
    average-method(["average method (Choice: medoid, non-metric-mean, non-metric-median)"]) --> beta-average
    distance-matrix-collection[["DistanceMatrix"]] --> beta-average
    beta-average{qiime boots beta-average} --> distance-matrix
    distance-matrix["DistanceMatrix"]
```

# Diagram key
```{mermaid}
flowchart LR
    action{Action}
    artifact[Artifact]
    artifact-collection[[Artifact collection]]
    parameter([parameter])
```

# `core-metrics` `Pipeline`

*I haven't got around to creating this one yet, but it's effectively a combination of the above three, except that the same resampled tables are used for all alpha and beta diversity metric calculations.*
