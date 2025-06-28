# Dockerfile
FROM debian:12

# Mise à jour et installation des outils nécessaires
RUN apt-get update && \
    apt-get install -y \
    freeradius-utils \
    iputils-ping \
    net-tools \
    curl \
    nano \
    vim \
    iproute2 && \
    apt-get clean

# Ajout d’un utilisateur non-root pour simuler un utilisateur normal
RUN useradd -ms /bin/bash clientuser

USER clientuser
WORKDIR /home/clientuser

# Entrée par défaut pour test manuel
CMD [ "bash", "-c", "while true; do sleep 3600; done" ]


