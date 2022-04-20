FROM jboss/wildfly

WORKDIR /opt/jboss/wildfly/standalone

USER root
RUN yum install -y graphviz curl wget
# Workaround because Ontobrowser searches "dot" in /usr/local/bin
RUN ln -s /usr/bin/dot /usr/local/bin/dot

# install apache-maven
RUN wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo \
    && yum clean metadata \
    && yum clean all \
    && yum install -y apache-maven
# RUN ln -s /usr/share/apache-maven/bin/mvn /usr/bin/mvn


# compile ontobrowser.war
RUN curl -s -S -O -L https://github.com/Novartis/ontobrowser/archive/master.zip \
    && unzip master.zip \
    && cd ontobrowser-master \
    && sed -i 's/return username/return "SYSTEM"/g' src/main/java/com/novartis/pcs/ontology/rest/servlet/OntologiesServlet.java \
    && sed -i 's/Oracle10gDialect/PostgreSQLDialect/g' src/main/resources/META-INF/persistence.xml \
    && mvn package \
    && cd .. \
    && cp ontobrowser-master/target/ontobrowser.war deployments/ \
    && rm ontobrowser-master master.zip -rf \
    && chown jboss deployments/ontobrowser.war

USER jboss
RUN wget https://jdbc.postgresql.org/download/postgresql-42.3.4.jar --no-check-certificate -O deployments/postgresql.jar
COPY standalone.xml configuration/

EXPOSE 9990 8080