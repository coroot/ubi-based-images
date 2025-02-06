FROM registry.k8s.io/kube-state-metrics/kube-state-metrics:v2.15.0 AS base

FROM registry.access.redhat.com/ubi9/ubi

LABEL name="kube-state-metrics" \
      vendor="Coroot, Inc." \
      maintainer="Coroot, Inc." \
      version=2.15.0 \
      release="1" \
      summary="Kube-state-metrics" \
      description="Kube-state-metrics UBI-based image."

COPY LICENSE /licenses/LICENSE

COPY --from=base /kube-state-metrics /kube-state-metrics

USER 65534:65534
EXPOSE 8080 8081
ENTRYPOINT ["/kube-state-metrics", "--port=8080", "--telemetry-port=8081"]
