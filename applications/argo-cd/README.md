# HA
- api server is stateless, so scaling is straightforward
  - may be worth setting ARGOCD_API_SERVER_REPLICAS to reduce calls to k8s api server
- repo server handles generating manifests, scale based on manifests generated and number of apps
  - set higher timeout for large manifets like istio and prometheus
- application controller is usually scaled based on cluster managed 1:1
  - may be worth setting ARGOCD_CONTROLLER_REPLICAS to reduce calls to k8s api serverPagIbig2023PasswordKo

# optimization
- reduce revision history, spec.revisionHistoryLimit
- use values files instead of putting it in the application resource
- disable storing health information in app crd, controller.resource.health.persist
- enable resource tree sharing, ARGOCD_APPLICATION_TREE_SHARD_SIZE=50
- take note of the orphaned resource monitoring feature
- resource exclusions like endpoint and endpointslice