FROM codercom/code-server:latest

USER coder

# Install NodeJS 
RUN curl -fsSL https://deb.nodesource.com/setup_15.x | sudo bash -
RUN sudo apt-get install -y git nodejs openjdk-11-jdk-headless
RUN npm config set prefix="/home/coder/.npm"
RUN echo "export PATH=$PATH:/home/coder/.npm/bin" >> /home/coder/.bashrc
RUN npm i -g sfdx-cli prettier prettier-plugin-apex

ENV SHELL=/bin/bash

# Install vscode extensions
RUN code-server --install-extension dbaeumer.vscode-eslint 
RUN code-server --install-extension esbenp.prettier-vscode
RUN code-server --install-extension salesforce.salesforcedx-vscode

# Install apt packages:
# RUN sudo apt-get install -y ubuntu-make

# Apply new VS Code settings
COPY settings.json .local/share/code-server/User/settings.json

# Start code-server into this folder instead
COPY entrypoint.sh /usr/bin/deploy-container-entrypoint.sh
ENTRYPOINT ["/usr/bin/deploy-container-entrypoint.sh"]
