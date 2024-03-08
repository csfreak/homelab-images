ARG NZBGET_VERSION
FROM ghcr.io/nzbgetcom/nzbget:${NZBGET_VERSION}

COPY --chown=0:0 --chmod=555 entrypoint.sh /


ENV NZBGET_CONFIG_OutputMode=log \
    NZBGET_CONFIG_WriteLog=none \
    NZBGET_CONFIG_ConfigTemplate=/nzbget/webui/nzbget.conf.template \
    NZBGET_CONFIG_ControlIP=0.0.0.0 \
    NZBGET_CONFIG_ControlPort=6789 \
    NZBGET_CONFIG_ControlUsername= \
    NZBGET_CONFIG_ControlPassword= \
    NZBGET_CONFIG_MainDir=/downloads \
    NZBGET_CONFIG_WebDir=/nzbget/webui/ \
    NZBGET_CONFIG_ErrorTarget=screen \
    NZBGET_CONFIG_WarningTarget=screen \
    NZBGET_CONFIG_InfoTarget=screen \
    NZBGET_CONFIG_DetailTarget=none

EXPOSE 6789
VOLUME /config
VOLUME /downloads

ENTRYPOINT [ "/entrypoint.sh" ]

CMD ["/app/nzbget/nzbget", "-s", "-c", "/config/nzbget.conf"]