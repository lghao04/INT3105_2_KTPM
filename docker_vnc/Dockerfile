FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Cài các gói cần thiết (gộp 1 RUN để tránh lỗi mạng)
RUN apt-get update && \
    apt-get install -y sudo wget vim net-tools \
                       xfce4 xfce4-terminal tightvncserver && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Tạo user docker
RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

USER docker
WORKDIR /home/docker

# Setup VNC
RUN mkdir -p /home/docker/.vnc && \
    echo "#!/bin/bash\nxrdb \$HOME/.Xresources\nstartxfce4 &" > /home/docker/.vnc/xstartup && \
    chmod +x /home/docker/.vnc/xstartup && \
    echo "1234\n1234\nn\n" | vncpasswd

EXPOSE 5901

CMD ["vncserver", ":1", "-geometry", "1280x800", "-depth", "24", "-fg"]
