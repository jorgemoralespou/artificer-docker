FROM jboss/wildfly:8.2.0.Final

MAINTAINER Brett Meyer <brmeyer@redhat.com>

ENV ARTIFICER_VERSION 1.0.0-SNAPSHOT

RUN cd $HOME \
  #&& curl http://downloads.jboss.org/artificer/artificer-$ARTIFICER_VERSION.zip | bsdtar -xvf- \
  #&& cd artificer-$ARTIFICER_VERSION \
  && curl https://repository.jboss.org/nexus/service/local/repositories/snapshots/content/org/artificer/artificer-distro-assembly/1.0.0-SNAPSHOT/artificer-distro-assembly-1.0.0-20150313.033203-16.zip | bsdtar -xvf- \
  && cd artificer-1.0.0-SNAPSHOT \
  && chmod 777 install.sh \
  && ./install.sh -Ds-ramp-distro.choices.platform=1 -Ds-ramp-distro.choices.platform.jboss-wildfly-8.path=$HOME/wildfly -Dejb-jms.password=artificer1! \
  && cp artificer-realm.json $HOME/wildfly \
  && cd .. \
  && rm -rf artificer*  

CMD ["wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-c", "standalone-full.xml", "-Dkeycloak.import=wildfly/artificer-realm.json"]
