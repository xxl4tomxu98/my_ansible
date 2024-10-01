FROM mcr.microsoft.com/devcontainers/python:1-3.12-bookworm
# install poetry for python dependencies
RUN python3 -m pip install poetry~=1.8.3
# enable bash completion for git
# RUN echo "source /usr/share/bash-completion/completions/git" >> ~/.bashrc

WORKDIR /workspaces/my_ansible

COPY poetry.lock pyproject.toml ./

RUN chown -R vscode:vscode /workspaces

USER vscode

RUN poetry install

# symlink poetry env to ~/venv
RUN VN=$(poetry env list | head -n 1 | cut -d ' ' -f 1) \
    && ln -s ~/.cache/pypoetry/virtualenvs/$VN ~/venv