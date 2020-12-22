FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install --no-install-recommends -y tigervnc-standalone-server firefox dbus-x11 xfce4 tigervnc-common

RUN useradd user && mkdir /home/user/ && chown user /home/user && usermod --shell /bin/bash user

USER user
RUN mkdir /home/user/.vnc

RUN echo "session=lxqt" >> /home/user/.vnc/config
RUN echo "geometry=1600x1000" >> /home/user/.vnc/config
RUN echo "localhost" >> /home/user/.vnc/config
RUN echo "alwaysshared" >> /home/user/.vnc/config

RUN echo "password" | vncpasswd -f > ~/.vnc/passwd && chmod 600 ~/.vnc/passwd

# LD_PRELOAD needed due to bug in tigervnc on arm.
# rm .X0 is needed since docker stop kills everything and lock file is left behind sometimes.
CMD ["/bin/bash", "-c", "rm -f /tmp/.X0* && LD_PRELOAD=/lib/aarch64-linux-gnu/libgcc_s.so.1 vncserver :0 -localhost no -fg"]