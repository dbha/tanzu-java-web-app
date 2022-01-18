
load('.tanzu/tanzu_tilt_extensions.py', 'tanzu_k8s_yaml')

SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", default='ghcr.io/dbha/tap/supply-chain/tanzu-java-web-app-demo')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')
NAMESPACE = os.getenv("NAMESPACE", default='demo')

custom_build('ghcr.io/dbha/tap/supply-chain/tanzu-java-web-app-demo',
    "tanzu apps workload apply --file config/workload.yaml --live-update \
      --local-path " + LOCAL_PATH + " --source-image " + SOURCE_IMAGE + " --namespace " + NAMESPACE + " --yes",
  ['pom.xml', './target/classes'],
  live_update = [
    sync('./target/classes', '/workspace/BOOT-INF/classes')
  ],
  skips_local_docker=True
)

allow_k8s_contexts('tap-private-cluster-admin@tap-private-cluster')
tanzu_k8s_yaml('tanzu-java-web-app-demo', 'ghcr.io/dbha/tap/supply-chain/tanzu-java-web-app-demo', './config/workload.yaml')

