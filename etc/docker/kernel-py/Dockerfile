# Ubuntu 18.04.1 LTS Bionic
FROM scipy-notebook-ppc64le

ENV PATH=$PATH:$CONDA_DIR/bin

RUN conda install --quiet --yes \
    cffi \
    ipykernel \
    ipython \
    jupyter_client \
    future \
    pycryptodomex && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

ADD ./kernel-launchers/bootstrap/bootstrap-kernel.sh /usr/local/bin
ADD ./kernel-launchers /usr/local/bin/kernel-launchers
ADD ./kernel-resources /usr/local/bin/
# ADD jupyter_enterprise_gateway_kernel_image_files*.tar.gz /usr/local/bin/

USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
    libkrb5-dev \
    && rm -rf /var/lib/apt/lists/*

RUN chown jovyan:users /usr/local/bin/bootstrap-kernel.sh && \
	chmod 0755 /usr/local/bin/bootstrap-kernel.sh && \
	chown -R jovyan:users /usr/local/bin/kernel-launchers

USER jovyan
ENV KERNEL_LANGUAGE python
CMD /usr/local/bin/bootstrap-kernel.sh
