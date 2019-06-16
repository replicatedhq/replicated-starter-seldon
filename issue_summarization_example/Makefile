VERSION=1.2
IMAGE_BASE=registry.replicated.com/seldonstarter/issue-summarization

push_rest:
	docker pull gcr.io/kubeflow-examples/issue-summarization-model@sha256:8457a5079f35f53442808af04520c0d45088240b7aed41cf4d5bfb9a9e02e792
	docker tag gcr.io/kubeflow-examples/issue-summarization-model@sha256:8457a5079f35f53442808af04520c0d45088240b7aed41cf4d5bfb9a9e02e792 ${IMAGE_BASE}:${VERSION}
	docker push ${IMAGE_BASE}:${VERSION}

