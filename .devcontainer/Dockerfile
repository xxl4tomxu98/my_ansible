FROM mcr.microsoft.com/devcontainers/python:1-3.12-bookworm
# OCI Labels
LABEL org.opencontainers.image.source="https://github.com/xxl4tomxu98/my_ansible"
LABEL org.opencontainers.image.description="Devcontainer Ansible "
LABEL org.opencontainers.image.licenses="GPL-3.0"
# install poetry for python dependencies
RUN python3 -m pip install poetry~=1.8.3
# install useful system packages
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y sshpass vim iputils-ping
RUN apt-get clean
# make prompt multiline cause it's too long by default
RUN sed -i -E -e '/PS1="\$/c\    PS1=" ${userpart} ${lightblue}\\w ${gitbranch}${removecolor}\\n\\$ "' ~/.bashrc
# enable bash completion for git
RUN echo "source /usr/share/bash-completion/completions/git" >> ~/.bashrc

WORKDIR /workspaces/my_ansible

COPY poetry.lock pyproject.toml .

# RUN chown -R vscode:vscode /workspaces

# USER vscode

RUN poetry install

# symlink poetry env to ~/venv
RUN VN=$(poetry env list | head -n 1 | cut -d ' ' -f 1) \
    && ln -s ~/.cache/pypoetry/virtualenvs/$VN ~/venv