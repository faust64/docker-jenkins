Klar Jenkins Agent
====================

https://github.com/openshift/jenkins lookalike

Based on https://github.com/optiopay/klar

scan:

```
CLAIR_ADDR=http://clair.project.svc:6060 \
	CLAIR_TIMEOUT=2 DOCKER_TIMEOUT=2 \
	DOCKER_USER=default \
	DOCKER_PASSWORD=$(cat /path/to/serviceaccount/token) \
	DOCKER_INSECURE=true \
	REGISTRY_INSECURE=false \
    klar docker-registry.default.svc:5000/project/jenkins-agent-klar:latest
```
