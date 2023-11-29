FROM ubuntu:latest AS base

WORKDIR /

RUN apt update
RUN apt install curl sudo wget -y
# Create a folder
RUN mkdir actions-runner && cd actions-runner

WORKDIR /actions-runner

# Download the latest runner package
RUN curl -o actions-runner-linux-x64-2.310.2.tar.gz -L https://github.com/actions/runner/releases/download/v2.310.2/actions-runner-linux-x64-2.310.2.tar.gz
# Optional: Validate the hash
# RUN echo "fb28a1c3715e0a6c5051af0e6eeff9c255009e2eec6fb08bc2708277fbb49f93  actions-runner-linux-x64-2.310.2.tar.gz" | shasum -a 256 -c
# Extract the installer
RUN tar xzf ./actions-runner-linux-x64-2.310.2.tar.gz

RUN wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
RUN sudo dpkg -i packages-microsoft-prod.deb
RUN rm packages-microsoft-prod.deb
RUN sudo apt-get update && sudo apt-get install -y dotnet-sdk-8.0

FROM base as withdotnetsdk

 ENTRYPOINT [ "./config.sh" ]
