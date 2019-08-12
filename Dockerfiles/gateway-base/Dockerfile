ARG PARENT_IMAGE
FROM $PARENT_IMAGE as builder

COPY APIGateway_Install.run /opt/APIGateway_Install.run
RUN cd /opt && \
    ./APIGateway_Install.run \
        --mode unattended \
        --unattendedmodeui none \
        --setup_type complete \
        --prefix /opt/Axway/ \
        --firstInNewDomain 0 \
        --configureGatewayQuestion 0 \
        --nmStartupQuestion 0 \
        --enable-components nodemanager,apimgmt \
        --disable-components analytics,apitester,policystudio,configurationstudio,qstart,cassandra \
        --startCassandra 0 && \
    rm -rf /opt/Axway/Axway-installLog.log \
        /opt/Axway/uninstall* \
        /opt/Axway/apigateway/upgrade \
        /opt/Axway/apigateway/docs \
        /opt/Axway/apigateway/Linux.x86_64/bin/wkhtmltopdf \
        /opt/Axway/apigateway/tools/filebeat* \
        /opt/Axway/apigateway/webapps/quickstart


FROM $PARENT_IMAGE
LABEL maintainer="support@axway.com"

RUN adduser emtuser -c "EMT User" && \
    chmod 777 /opt
COPY --chown=emtuser --from=builder /opt/Axway /opt/Axway