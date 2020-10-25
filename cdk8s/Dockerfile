ARG ARGOCD_VERSION

FROM argoproj/argocd:$ARGOCD_VERSION

ARG CDK8S_VERSION

USER root

RUN set -x; \
    apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && bash -c 'curl -sL https://deb.nodesource.com/setup_lts.x | bash -' \
    && apt-get install -y nodejs \
    && bash -c 'curl -L https://raw.githubusercontent.com/pnpm/self-installer/master/install.js | node' \
    && ln -f -s $(which pnpm) $(which npm) \
    && pnpm install -g cdk8s-cli@$CDK8S_VERSION \
    && mkdir -p /tmp/example \
    && (cd /tmp/example && cdk8s init typescript-app) \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN npm version

USER argocd
