FROM gcr.io/cloud-marketplace-tools/k8s/deployer_envsubst:0.7.0

ARG KYMA_VERSION
ENV KYMA_VERSION ${KYMA_VERSION}
ARG DEPLOYER_VERSION
ENV DEPLOYER_VERSION ${DEPLOYER_VERSION}
ARG KYMA_INITIALIZER_IMAGE

ADD manifest/* /data/manifest/
ADD schema.yaml /data/

RUN cat /data/schema.yaml \
    | env -i "KYMA_INITIALIZER_IMAGE=$KYMA_INITIALIZER_IMAGE" envsubst \
    > /data/schema.yaml.new \
    && mv /data/schema.yaml.new /data/schema.yaml \
    && cat /data/manifest/application.yaml \
    | sed "s/\$VERSION/${DEPLOYER_VERSION}/g" \
    > /data/manifest/application.yaml.new \
    && mv /data/manifest/application.yaml.new /data/manifest/application.yaml
