FROM paxi-quorum_paxi-node

RUN echo "deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/" > /etc/apt/sources.list.d/cran-focal.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update
RUN apt-get install -y r-base
RUN apt-get install -y r-base-dev

# for forecast package
RUN apt-get install -y libcurl4-openssl-dev

RUN Rscript -e 'install.packages("Rserve",, "http://rforge.net/")'
RUN Rscript -e 'install.packages("tidyverse")'
RUN Rscript -e 'install.packages("tsibble")'
RUN Rscript -e 'install.packages("fable")'
RUN Rscript -e 'install.packages("fable.prophet")'
RUN Rscript -e 'install.packages("feasts")'
RUN Rscript -e 'install.packages("forecast")'

RUN apt-get install -y git
RUN apt-get install -y autoconf
RUN swipl -g "pack_install(rserve_client, [interactive(false)])" -g "pack_rebuild(rserve_client)"

WORKDIR /srv
COPY srv .

# https://svn.r-project.org/R/trunk/src/library/base/R/namespace.R
ENV _R_S3_METHOD_REGISTRATION_NOTE_OVERWRITES_=0
