FROM gcr.io/tensorflow/tensorflow:latest-gpu
MAINTAINER James Gabriel <James.C.Gabriel@disney.com>
RUN apt-get update
RUN rm -rf /notebooks/*
ADD *.ipynb /notebooks/
WORKDIR /notebooks
CMD ["/run_jupyter.sh"
