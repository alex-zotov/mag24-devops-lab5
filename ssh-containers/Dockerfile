FROM ubuntu:24.04

RUN apt-get update && \
    apt-get install -y openssh-server sudo curl && \
    mkdir -p /var/run/sshd

RUN apt-get install -y iputils-ping

RUN echo 'PermitRootLogin no' >> /etc/ssh/sshd_config && \
    echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config && \  
    echo 'PubkeyAuthentication yes' >> /etc/ssh/sshd_config 

# создание пользователя runner
# -m: Создает домашний каталог
RUN useradd -m -s /bin/bash runner && \
    echo 'runner:runnerpass' | chpasswd && \
    # Добавляем в группу sudo 
    usermod -aG sudo runner

# Даём runner право на sudo без пароля (опционально)
RUN echo 'runner ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Открытие порта SSH
EXPOSE 22

# Запуск SSH-сервера
#CMD ["/usr/sbin/sshd", "-D"]
