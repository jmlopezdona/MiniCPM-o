# Image container to run backend api server of minicpm-o_2.6 webserver
# To build image: docker build -t minicpm-o_2.6-api-server:latest .
# To run contaniner: docker run --gpus all -it --rm -p 32550:32550 minicpm-o_2.6-api-server:latest
FROM pytorch/pytorch:2.3.1-cuda12.1-cudnn8-devel

# Set environment variables
ENV CUDA_HOME=/usr/local/cuda \
    PATH=/usr/local/cuda/bin:$PATH \
    LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH

# Update system and install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libtorch-dev \
    python3-dev \
    python3-pip \
    git \
    curl \
    wget && \
    rm -rf /var/lib/apt/lists/*

# Install Python packages
RUN pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
RUN pip install flash_attn

# Clone and set up MiniCPM-o
RUN cd ~ && \
    git clone https://github.com/jmlopezdona/MiniCPM-o.git && \
    cd MiniCPM-o && \
    pip install -r requirements_o2.6.txt

# Set working directory
WORKDIR /root/MiniCPM-o

# Pre-run the script to download necessary files
RUN python web_demos/minicpm-o_2.6/model_server.py || true

# Expose port for external access
EXPOSE 32550

CMD ["python", "web_demos/minicpm-o_2.6/model_server.py"]
