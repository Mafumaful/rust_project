# Use Rust slim image as the base
FROM rust:slim-bullseye as base

# Create a development stage from the base image
FROM base as dev

# >>>>>>>>>>>>>>>>>>>>>>>>> User Settings >>>>>>>>>>>>>>>>>>>>>>>>>

# Set environment variables
ENV USER=docker

# Update the package list and install necessary packages
RUN apt-get update && apt-get install -y sudo zsh wget git curl

# Create a new user and add it to the sudo group
RUN useradd -m ${USER} && echo "${USER}:${USER}" | chpasswd && adduser ${USER} sudo

# Give the user passwordless sudo privileges
RUN echo "${USER} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Set zsh as the default shell for the user
RUN chsh -s /bin/zsh ${USER}

# Switch to the new user
USER ${USER}:${USER}

# >>>>>>>>>>>>>>>>>>>>>>>>> Directory Setup >>>>>>>>>>>>>>>>>>>>>>>>>

# Create a working directory for the user
RUN mkdir -p /home/${USER}/code
WORKDIR /home/${USER}/code

# >>>>>>>>>>>>>>>>>>>>>>>>> oh-my-zsh Setup >>>>>>>>>>>>>>>>>>>>>>>>>

# Install oh-my-zsh for the user
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended

# Set the default shell to zsh
CMD [ "zsh" ]
