# fluent-bit

## How to use ?

1. Add fluentd centralize in `fluentd-bit-configmap.yaml`
```
  output-fluentd.conf: |
    [OUTPUT]
        Name                forward
        Match               *
        Host                your-fluentd-centralize
        Port                24224
        Retry_Limit         False
        tls                 off
        tls.verify          off
```

2. Replace your docker data path at volume/volumeMount in `fluentd-bit-ds.yaml`
```
    volumeMounts:
    # hostpath must be the same with mountpath -> https://github.com/kubernetes/minikube/issues/876
    - name: varlibdockercontainers
      mountPath: "your docker/data/containers path"
      readOnly: false
    ...
    ...
  volumes:
    ...
  - name: varlibdockercontainers
    hostPath:
      path: "your docker/data/containers path"
```



## Manifest for fluent-bit daemonset.

This is simple fluent-bit daemonset sending all docker containers log to another Fluentd/Fluent-bit Centralize instance.

## Why don't we directly send logs to ES/KAFKA ? 

The Centralize instance will work like a queue, keep your logs safe when ES/Kafka broken and can filter or send your logs to any destination like Bigquery/Kafka... with @type support.

## Debug 

Change image from `version` to `version-debug` for execution shell in to container.

Example: `image: fluent/fluent-bit:1.3.5` -> `image: fluent/fluent-bit:1.3.5-debug`
