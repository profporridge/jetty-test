FROM jetty
RUN java -jar "$JETTY_HOME/start.jar" --add-to-startd=jmx,stats
USER jetty
COPY jmx-exporter.yaml ${JETTY_BASE}/
RUN curl https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.12.0/jmx_prometheus_javaagent-0.12.0.jar \
    --output ${JETTY_BASE}/jmx_prometheus_javaagent-0.12.0.jar
WORKDIR ${JETTY_BASE}
CMD java -javaagent:${JETTY_BASE}/jmx_prometheus_javaagent-0.12.0.jar=9093:${JETTY_BASE}/jmx-exporter.yaml \
         -jar ${JETTY_HOME}/start.jar