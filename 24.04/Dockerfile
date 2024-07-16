FROM ubuntu:24.04

# install all recomand tools
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    vim \
    nano \
    unzip \
    zip \
    python3 \
    python3-pip \
    python3-venv \
    python3-dev \
    build-essential \
    adduser \
    gcc \
    g++ \
    && rm -rf /var/lib/apt/lists/*

# download tools for pwn
RUN apt-get update && apt-get install -y \
    gdb \
    gdbserver \
    ltrace \
    strace \
    nasm \
    socat \
    netcat-traditional \
    && rm -rf /var/lib/apt/lists/*

RUN python3 -m pip config set global.break-system-packages true
RUN pip3 install pwntools

# download onegadget, ropgadget, seccomp-tools
RUN apt-get update && apt-get install -y \
    ruby \
    ruby-dev \
    && rm -rf /var/lib/apt/lists/*

RUN gem install one_gadget
RUN python3 -m pip install ROPgadget
RUN gem install seccomp-tools

# add user qwerty
RUN adduser qwerty

# install rp++
RUN wget https://github.com/0vercl0k/rp/releases/download/v1/rp-lin-x86 -O /home/qwerty/rp86
RUN wget https://github.com/0vercl0k/rp/releases/download/v2.0.2/rp-lin-x64 -O /home/qwerty/rp64
RUN chmod +x /home/qwerty/rp86 /home/qwerty/rp64

# install bata24 gef
RUN wget https://raw.githubusercontent.com/bata24/gef/dev/gef.py -O /home/qwerty/.gdbinit-gef.py
RUN echo "source ~/.gdbinit-gef.py" >> /home/qwerty/.gdbinit

# install sudo & setting source debugging
RUN apt-get update && apt-get -y install sudo libc6-dbg glibc-source xz-utils
RUN xz -d -v /usr/src/glibc/glibc-2.??.tar.xz
RUN mkdir /usr/src/glibc/source
RUN tar -xvf /usr/src/glibc/glibc-2.??.tar -C /usr/src/glibc/source
RUN cp -r /usr/src/glibc/source/glibc-2.??/* /usr/src/glibc/source

RUN echo "dir /usr/src/glibc/source" >> /home/qwerty/.gdbinit

# set default user
USER qwerty

# hold infinite
ENTRYPOINT ["tail", "-f", "/dev/null"]