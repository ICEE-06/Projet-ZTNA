# Dockerfile
FROM debian:12

ENV DEBIAN_FRONTEND=noninteractive

# Installation de FreeRADIUS et outils de debug
RUN apt-get update && \
    apt-get install -y \
    freeradius \
    freeradius-utils \
    iputils-ping \
    nano \
    vim \
    net-tools \
    curl && \
    apt-get clean

# Copie du fichier users (ajout d'un utilisateur test)
COPY users /etc/freeradius/3.0/mods-config/files/authorize

# Copie du fichier clients.conf (ajout des clients autorisés)
COPY clients.conf /etc/freeradius/3.0/clients.conf

# Port RADIUS UDP 1812
EXPOSE 1812/udp

# Lancement de FreeRADIUS en mode foreground (debug log dans terminal)
CMD ["freeradius", "-X"]
