FROM openjdk:8

RUN wget https://netix.dl.sourceforge.net/project/pentaho/Pentaho%208.3/client-tools/pdi-ce-8.3.0.0-371.zip
RUN unzip pdi-ce-8.3.0.0-371.zip
RUN mv data-integration /opt/
COPY mysql-connector-java-5.1.48.jar /opt/data-integration/lib/mysql-connector-java-5.1.48.jar
COPY mysql-connector-java-5.1.48-bin.jar /opt/data-integration/lib/mysql-connector-java-5.1.48-bin.jar


RUN apt-get update 
RUN apt-get install -y libwebkitgtk-1.0-0 
RUN apt-get install -y sudo
RUN apt-get install -y libxtst6

# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer
CMD /opt/data-integration/spoon.sh