# Use miniconda image base from Dockerhub
FROM continuumio/miniconda3

# Metadata
LABEL container.base.image = "miniconda3:python3.9"
LABEL software.name = "macs2"

# Install system packages and AWS CLI
RUN apt-get -y update && \
    apt-get -y install python3-pip
RUN pip install awscli boto3 MACS2
# RUN conda install -c bioconda macs2

WORKDIR /

# copy relevant scripts to root dir
RUN mkdir -p global_utils/src
COPY src/run_main.py /
COPY src/global_utils/src/module_utils.py /global_utils/src/
COPY src/global_utils/src/file_utils.py /global_utils/src/
COPY src/global_utils/src/global_keys.py /global_utils/src/
COPY src/global_utils/src/aws_s3_utils.py /global_utils/src/
ENV PATH="/usr/local/bin/:$PATH"

ENTRYPOINT ["python","/run_main.py"] 
