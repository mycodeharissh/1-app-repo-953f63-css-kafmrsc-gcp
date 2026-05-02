"# 1-app-repo-953f63-css-kafmrsc-gcp" 
🚀 Deployment Order
Deploy in this sequence:
StepFolderReason
1. **crds** Must be first — registers Custom Resource Definitions so Kubernetes understands Confluent resource types
2. **operator** Confluent Operator must exist before any Confluent resources are created
3. **certificates** TLS certs must be ready before any component tries to use them
4. **kraftcontroller** KRaft controller replaces ZooKeeper — brokers depend on it
5. **kafka** Brokers come up after the KRaft controller is healthy
6. **schemaregistry** Depends on Kafka being available
7. **connect** Kafka Connect depends on Kafka (and optionally Schema Registry)
8. **controlcenter** Control Center monitors everything — deploy last so it has all components to connect to
9. **clusterlink** ClusterLink bridges clusters — deploy after both source and destination Kafka are up