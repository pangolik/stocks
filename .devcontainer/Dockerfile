# Use the base image with the specified GLUE_VERSION
ARG GLUE_VERSION="4.0.0"
FROM amazon/aws-glue-libs:glue_libs_${GLUE_VERSION}_image_01

# Set the user to glue_user
ARG USER=glue_user
USER $USER

# Set the home directory
ARG HOME="/home/$USER"
ENV PATH="${HOME}/.local/bin:$PATH"

# Install Git
USER root
RUN yum install -y git

# Install sudo
RUN yum install -y sudo

# Add glue_user to sudoers with root permissions
RUN echo "${USER} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Install Python dependencies from requirements.txt (if the file exists)
COPY requirements.txt .
RUN if [ -f "requirements.txt" ]; then \
    echo "Installing Python dependencies" \
    && pip3 install -r requirements.txt; \
    fi

RUN pip3 install google-api-python-client

USER $USER