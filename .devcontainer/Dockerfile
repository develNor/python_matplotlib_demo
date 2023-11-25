# Use the official image for ROS Noetic under Ubuntu 20.04
FROM ubuntu:22.04


####################################################################################################
############# Use Non Root User ####################################################################
####################################################################################################

# Add non-root user
ENV USERNAME=myuser
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && apt-get update \
  && apt-get -y install sudo \
   # [Optional] Add sudo support for the non-root user
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
  && chmod 0440 /etc/sudoers.d/$USERNAME \
   # Clean up
  && rm -rf /var/lib/apt/lists/*

# Use the non-root user in this script
USER ${USERNAME}:${USERNAME}

WORKDIR /home/${USERNAME}/


####################################################################################################
############# Install Container Setup ##############################################################
####################################################################################################

# install matplotlib
RUN sudo apt-get update && sudo apt-get -y install \
    python3-pip \
  && sudo rm -rf /var/lib/apt/lists/*
RUN pip install matplotlib
# install tk which ist required to create plots with matplotlib 
RUN sudo apt-get update && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install \
   python3-tk \
  && sudo rm -rf /var/lib/apt/lists/*

# enable jupyter notebooks which require the following dependency
RUN pip install ipykernel