FROM jefferys/bioconductor:3.10_latest

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      build-essential \
      libtool \
      m4 \
      automake \
      autoconf \
      git \
      bison \
      flex \
      python3 \
      python3-dev \
      python3-numpy \
      python3-pip \
      python3-psutil \
      python3-pybind11 \
      python3-setuptools \
      python3-wheel

RUN pip3 install \
      python-igraph \
      leidenalg

RUN pip3 install nmslib==2.0.5

RUN R -e 'BiocManager::install( \
    c( "flowCore", "data.table", "RANN", "Rcpp", "RcppParallel", \
       "igraph", "nmslibR", "mclust", "MLmetrics", "remotes" ), \
    update= FALSE, \
    ask= FALSE, \
    version= "3.10" \
)'

# Wrapping grappolo into R code
# RUN /usr/bin/curl -L "https://hpc.pnl.gov/people/hala/files/grappolo.tar.gz" \
#                  -o "/usr/local/grappolo.tar.gz" && \
#    cd "/usr/local" && \
#    mkdir "grappolo-latest" && \
#    tar -zxvf "grappolo.tar.gz" -C grappolo-latest --strip-components=1 && \
#    rm "grappolo.tar.gz" && \
#    cd "grappolo-latest" && \
#    make && \
#    cp driverForGraphClustering /usr/local/bin/ && \
#    cd .. && \
#    rm -r /usr/local/grappolo-latest

RUN R -e 'BiocManager::install( \
    c( "sararselitsky/FastPG" ), \
    update= FALSE, \
    ask= FALSE, \
    version= "3.10" \
)'

# At end as args breaks all following caching. Timestamp changes every time...

ARG imageCreated
ARG toolVersion

ARG toolSource="https://github.com/sararselitsky/FastPG/tree/dev"
ARG tool="fastpg"
ARG brief="${tool} - Container for running the R package FastPG."
ARG toolLicense="MIT"

# From https://github.com/opencontainers/image-spec/blob/master/annotations.md
LABEL org.opencontainers.image.created="${imageCreated}"
LABEL org.opencontainers.image.authors="Stuart R. Jefferys <srj@unc.edu>"
LABEL org.opencontainers.image.url="https://hub.docker.com/r/jefferys/${tool}"
LABEL org.opencontainers.image.source="https://github.com/jefferys/Dockers/ToolDockers/${tool}"
LABEL org.opencontainers.image.version="${toolVersion}"
LABEL org.opencontainers.image.vendor="UNC - Lineberger"
LABEL org.opencontainers.image.licenses="${toolLicense}"
LABEL org.opencontainers.image.title="${brief}"
LABEL org.opencontainers.image.description="The fastpg R package for clustering large sample sets (millions) with intermediate features (order of 100). Includes source from Grappolo, BSD-3 licensed from Pacific Northwest National Laboratory"

# https://github.com/BioContainers/specs/blob/master/container-specs.md
LABEL base_image="jefferys/bioconductor:3.10_latest"
LABEL version="${toolVersion}"
LABEL software.version="${toolVersion}"
LABEL software="${tool}"
LABEL about.summary="${brief}"
LABEL about.home="${toolSource}"
LABEL about.license="${toolLicense}"
LABEL about.tags="debian, bioconductor, fastpg, nlmlib"
LABEL maintainer="Stuart R. Jefferys <srj@unc.edu>"

ENV RETICULATE_PYTHON=/usr/bin/python3

CMD ["bash"]
