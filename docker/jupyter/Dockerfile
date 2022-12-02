FROM jupyter/minimal-notebook

USER root

RUN apt-get -y update && \
    apt-get install --no-install-recommends -y \
      curl \
      openjdk-11-jre-headless \
      ca-certificates-java \
      ssh \
      dnsutils \
      iputils-ping \
      git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID
WORKDIR /home/vibhavangadi/work

# Install java kernel
RUN git clone https://github.com/SpencerPark/IJava.git && \
    cd IJava/ && \
    chmod u+x gradlew && ./gradlew installKernel
ADD kernel.json /home/vibhavangadi/.local/share/jupyter/kernels/java/kernel.json

# download project
RUN git clone https://github.com/VibhavAngadi/BIG_DATA_Project.git


# ssh config
RUN mkdir /home/vibhavangadi/.ssh
COPY ssh/id_rsa /home/vibhavangadi/.ssh/
COPY ssh/id_rsa.pub /home/vibhavangadi/.ssh/
COPY ssh/public-keys /home/vibhavangadi/.ssh/authorized_keys
COPY ssh/ssh-config /home/vibhavangadi/.ssh/config

USER root
RUN chown -R user: /home/vibhavangadi/.ssh

USER $NB_UID
