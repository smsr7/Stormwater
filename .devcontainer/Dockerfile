#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See https://go.microsoft.com/fwlink/?linkid=2090316 for license information.
#-------------------------------------------------------------------------------------------------------------

FROM python:3

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

# Copy requirements.txt (if found) to a temp locaition so we can install it. Also
# copy "noop.txt" so the COPY instruction does not fail if no requirements.txt exists.
COPY requirements.txt* .devcontainer/noop.txt /tmp/pip-tmp/

# Configure apt and install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils 2>&1 \
    #
    # Verify git, process tools, lsb-release (common in install instructions for CLIs) installed
    && apt-get -y install git procps lsb-release
    #
    # Install pylint
RUN pip install pylint
RUN pip install keras==2.2.4 \
&& pip install numpy==1.16.4 \ 
&& pip install pyswmm==0.4.8 \
&& pip install tensorflow_gpu==1.14.0 \
&& pip install gym \ 
&& pip install matplotlib
#&& if [ -f "/tmp/pip-tmp/requirements.txt" ]; then pip install -r /tmp/pip-tmp/requirements.txt; fi \
    #&& rm -rf /tmp/pip-tmp \
   #
    #
    # Clean up
RUN command apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog


