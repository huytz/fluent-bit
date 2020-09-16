# fluent-bit

## Manifest for fluent-bit daemonset.
This is simple fluent-bit daemonset sending all docker containers log to another Fluentd/Fluent-bit Centralize instance.

## Why don't we directly send logs to ES/KAFKA? 
The Centralize instance will work like a queue, keep your logs safe when ES/Kafka broken and can filter or send your logs to any destination like Bigquery/Kafka... with @type support.