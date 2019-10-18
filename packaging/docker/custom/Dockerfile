ARG GRAFANA_VERSION="latest"

FROM grafana/grafana:${GRAFANA_VERSION}

USER grafana

ARG GF_INSTALL_PLUGINS=""

RUN if [ ! -z "${GF_INSTALL_PLUGINS}" ]; then \
    OLDIFS=$IFS; \
        IFS=','; \
    for plugin in ${GF_INSTALL_PLUGINS}; do \
        IFS=$OLDIFS; \
        grafana-cli --pluginsDir "$GF_PATHS_PLUGINS" plugins install ${plugin}; \
    done; \
fi

RUN if [ ! -z "${GF_INSTALL_PLUGINS_URL}" ]; then \
    OLDIFS=$IFS; \
    IFS=','; \
    for plugin_url in ${GF_INSTALL_PLUGINS_URL}; do \
	      plugin=''; \
	      url=''; \
	      n=0; \
        IFS=';'; \
	      for val in ${plugin_url}; do \
		        if [ $n -eq 0 ]; \
		        then \
			          url=$val; \
			          n=1; \
		        else \
			          plugin=$val; \
			          break; \
		        fi; \
	      done; \
        IFS=$OLDIFS; \
        grafana-cli --pluginsDir "$GF_PATHS_PLUGINS" --pluginUrl ${url} plugins install ${plugin}; \
    done; \
fi
