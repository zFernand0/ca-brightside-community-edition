# This Dockerfile is used to build an image capable of running brightside 2.0 commands
FROM zfernand0/jenkins-nvm-agent
ARG PKG_TAG='latest'

# Sets the scoped registry for brightside packages
USER jenkins

# Setup registries
RUN npm config set @brightside:registry https://api.bintray.com/npm/ca/brightside
RUN npm config set @zowe:registry
RUN npm config set @broadcom:registry

# Focusing on latest and zowe-v1-lts
RUN if [ "$PKG_TAG" = "latest" ] || [ "$PKG_TAG" = "zowe-v1-lts" ]; then \
    # Zowe CLI first
    npm install -g @zowe/cli@$PKG_TAG; \
    # Then the Zowe available plugins
    zowe plugins install @zowe/cics-for-zowe-cli@$PKG_TAG; \
    zowe plugins install @zowe/mq-for-zowe-cli@$PKG_TAG; \
    zowe plugins install @zowe/ims-for-zowe-cli@$PKG_TAG; \
    zowe plugins install @zowe/db2-for-zowe-cli@$PKG_TAG; \
    zowe plugins install @zowe/secure-credential-store-for-zowe-cli@$PKG_TAG; \
    # And Broadcom public packages
    zowe plugins install @broadcom/endevor-for-zowe-cli@$PKG_TAG; \
    zowe plugins install @broadcom/file-master-plus-for-zowe-cli@$PKG_TAG; \
    zowe plugins install @broadcom/ops-for-zowe-cli@$PKG_TAG; \
    zowe plugins install @broadcom/caview-for-zowe-cli@$PKG_TAG; \
    fi

RUN if [ "$PKG_TAG" = "lts-incremental" ]; then \
    # First the Brightside CLI
    npm install -g @brightside/core@$PKG_TAG; \
    # Then the Brightside available plugins
    zowe plugins install @brightside/cics@$PKG_TAG; \
    zowe plugins install @brightside/db2@$PKG_TAG; \
    zowe plugins install @brightside/endevor@$PKG_TAG; \
    zowe plugins install @brightside/filemasterplus@$PKG_TAG; \
    zowe plugins install @brightside/ops@$PKG_TAG; \
    zowe plugins install @brightside/zos-extended-files@$PKG_TAG; \
    zowe plugins install @brightside/zos-extended-jobs@$PKG_TAG; \
    zowe plugins install @brightside/secure-credential-store@$PKG_TAG; \
    fi

USER root