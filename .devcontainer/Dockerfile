# Dockerfile
FROM nvidia/cuda:11.6.1-devel-ubuntu20.04

ENV PYTHON_VERSION=3

ENV LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:/usr/local/lib"

ENV PYTHONIOENCODING=UTF-8
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV DEBIAN_FRONTEND=noninteractive

RUN apt update
RUN apt install -y bash \
    build-essential \
    git \
    curl \
    ca-certificates \
    wget \
    python${PYTHON_VERSION} \
    python${PYTHON_VERSION}-pip \
    && rm -rf /var/lib/apt/lists

RUN python3 -m pip install --upgrade pip --trusted-host pypi.org --trusted-host files.pythonhosted.org

# Install requirements
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt \
    && rm requirements.txt

# Create a user named 'dinov2' with sudo permissions
RUN useradd -m -s /bin/bash dinov2 && \
    echo 'dinov2 ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Switch to the 'dinov2' user
USER dinov2

# Set the working directory
WORKDIR /home/dinov2

CMD ["/bin/bash"]
