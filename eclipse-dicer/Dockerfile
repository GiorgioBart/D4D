FROM ubuntu:14.04


ENV ECLIPSE_FILE eclipse-java-neon-1a-linux-gtk-x86_64.tar.gz
ENV ECLIPSE_FILE_URL http://eclipse.c3sl.ufpr.br/technology/epp/downloads/release/neon/1a/$ECLIPSE_FILE

#RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
#    apt-get update && \
#    apt-get install -yq --no-install-recommends software-properties-common && \
#    add-apt-repository ppa:webupd8team/java -y && apt-get update && \
#    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
#    apt-get install -yq --no-install-recommends oracle-java8-installer && \
#    wget $ECLIPSE_FILE_URL -O /tmp/eclipse.tar.gz -q && \
#    tar -xf /tmp/eclipse.tar.gz -C /opt && rm /tmp/eclipse.tar.gz

#Istalling Java and Eclipse
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get install -yq --no-install-recommends openjdk-8-jdk && \
    wget $ECLIPSE_FILE_URL -O /tmp/eclipse.tar.gz -q && \
    tar -xf /tmp/eclipse.tar.gz -C /opt && rm /tmp/eclipse.tar.gz

#Adding Eclipse's PlugIn
RUN /opt/eclipse/eclipse \
    -nosplash \
    -application org.eclipse.equinox.p2.director \
    -repository http://download.eclipse.org/ecoretools/updates/releases/3.1.0/neon \
     -installIU  org.eclipse.emf.ecoretools.explorer.contextual.feature.group/3.1.0.201605311155 \
     -installIU  org.eclipse.emf.ecoretools.design.feature.group/3.1.0.201605311155 \
     -installIU  org.eclipse.emf.ecoretools.sdk.feature.group/3.1.0.201605311155 \
    -repository http://download.eclipse.org/modeling/emf/updates/releases/ \
     -installIU  org.eclipse.emf.examples.source.feature.group/2.4.0.v200902171115 \
     -installIU  org.eclipse.emf.ecore.sdo.feature.group/2.4.0.v200902171115 \
     -installIU  org.eclipse.emf.ecore.sdo.doc.feature.group/2.4.0.v200902171115 \
     -installIU  org.eclipse.emf.ecore.sdo.edit.feature.group/2.4.0.v200902171115 \
     -installIU  org.eclipse.emf.ecore.sdo.editor.feature.group/2.4.0.v200902171115 \
     -installIU  org.eclipse.emf.ecore.sdo.sdk.feature.group/2.4.0.v200902171115 \
     -installIU  org.eclipse.emf.ecore.sdo.source.feature.group/2.4.0.v200902171115 \
    -repository http://download.eclipse.org/modeling/gmp/gmf-runtime/updates/releases/ \
     -installIU  org.eclipse.gmf.examples.runtime.feature.group/1.10.0.201606071959 \
     -installIU  org.eclipse.gmf.examples.runtime.ui.pde.feature.group/1.10.0.201606071959 \
     -installIU  org.eclipse.gmf.runtime.sdk.feature.group/1.10.0.201606071959 \
     -installIU  org.eclipse.gmf.source.feature.group/1.10.0.201606071959 \
     -installIU  org.eclipse.gmf.tests.runtime.feature.group/1.10.0.201606071959 \
     -installIU  org.eclipse.gmf.runtime.thirdparty.source.feature.group/1.10.0.201606071959 \
    -repository http://download.eclipse.org/releases/neon \
     -installIU  org.eclipse.xsd.feature.group/2.12.0.v20160526-0356 \
     -installIU  org.eclipse.xsd.ecore.converter.feature.group/2.9.0.v20160526-0356 \
     -installIU  org.eclipse.xsd.edit.feature.group/2.9.0.v20160526-0356 \
     -installIU  org.eclipse.xsd.sdk.feature.group/2.12.0.v20160526-0356 \
     -installIU  org.eclipse.xsd.mapping.feature.group/2.9.0.v20160526-0356 \
     -installIU  org.eclipse.xsd.mapping.editor.feature.group/2.9.0.v20160526-0356 \
    -destination /opt/eclipse/

#Adding package for X11
RUN apt-get install -y --no-install-recommends \
         libxext-dev \
         libxrender-dev \
         libxtst-dev \
         libgtk2.0-0 \
         libcanberra-gtk-module \
         light-themes \
         git \
         unzip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    
#    rm -rf /usr/lib/jvm/java-8-oracle/lib/missioncontrol && \
#    rm -rf /usr/lib/jvm/java-8-oracle/lib/visualvm

ADD run /usr/local/bin/eclipse
ADD net.sourceforge.dynamicgmf.diagram_0.2.1.jar /opt/eclipse/dropins/
#ADD com.seeq.eclipse.importprojects_1.3.0.jar /opt/eclipse/plugins/
ADD D4D /opt/D4D

RUN chmod +x /usr/local/bin/eclipse && \
    mkdir -p /home/dicer && \
    echo "dicer:x:1000:1000:DICER,,,:/home/dicer:/bin/bash" >> /etc/passwd && \
    echo "dicer:x:1000:" >> /etc/group && \
    echo "dicer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/dicer && \
    chmod 0440 /etc/sudoers.d/dicer && \
    wget https://github.com/DICERs/DICER/releases/download/v0.1.0/dicer-full.zip -P /home/dicer && \
    wget https://github.com/seeq12/eclipse-import-projects-plugin/blob/master/jar/com.seeq.eclipse.importprojects_1.3.0.jar -P /opt/eclipse/plugins/ && \
    unzip /home/dicer/dicer-full.zip -d /home/dicer && \
    cp -R /home/dicer/dicer-core/models /opt/D4D && \
    cp -R /home/dicer/dicer-core/metamodels /opt/D4D && \
    chown dicer:dicer -R /home/dicer && \
    chown root:root /usr/bin/sudo && chmod 4755 /usr/bin/sudo


USER dicer
ENV HOME /home/dicer
WORKDIR /home/dicer
CMD /usr/local/bin/eclipse
