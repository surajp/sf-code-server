FROM codercom/code-server:latest

USER coder

# Install NodeJS 12.x
RUN curl -fsSL https://deb.nodesource.com/setup_15.x | sudo bash -
RUN sudo apt-get install -y git nodejs openjdk-11-jdk-headless
RUN npm config set prefix="/home/code/.npm"
RUN echo "export PATH=$PATH:/home/code/.npm/bin" >> /home/code/.bashrc
npm i -g sfdx-cli prettier prettier-plugin-apex

ENV SHELL=/bin/bash

RUN sudo chown -R coder:coder /home/coder/.local

# Install linter
RUN code-server --install-extension dbaeumer.vscode-eslint esbenp.prettier-vscode salesforce.salesforcedx-vscode --extensions-dir /home/coder/.local/share/code-server/extensions

# Install apt packages:
# RUN sudo apt-get install -y ubuntu-make

# Apply new VS Code settings
COPY settings.json .local/share/code-server/User/settings.json

# Start code-server into this folder instead
COPY entrypoint.sh /usr/bin/deploy-container-entrypoint.sh
ENTRYPOINT ["/usr/bin/deploy-container-entrypoint.sh"]
