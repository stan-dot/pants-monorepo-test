# This file is for use as a devcontainer and a runtime container
#
# The devcontainer should use the build target and run as root with podman
# or docker with user namespaces.
#
FROM python:3.11 as build

ARG PIP_OPTIONS=.

# Add any system dependencies for the developer/build environment here e.g.
# RUN apt-get update && apt-get upgrade -y && \
#     apt-get install -y --no-install-recommends \
#     desired-packages \
#     && rm -rf /var/lib/apt/lists/*

# set up a virtual environment and put it in PATH
RUN python -m venv /venv
ENV PATH=/venv/bin:$PATH

# Copy any required context for the pip install over
COPY . /context
WORKDIR /context

# install python package into /venv
RUN pip install ${PIP_OPTIONS}

FROM python:3.11 as runtime

# Add apt-get system dependecies for runtime here if needed

# copy the virtual environment from the build stage and put it in PATH
COPY --from=build /venv/ /venv/
COPY ./container-startup.sh /container-startup.sh
ENV PATH=/venv/bin:$PATH


RUN mkdir -p /.cache/pip; chmod -R 777 /venv /.cache/pip

# change this entrypoint if it is not the same as the repo
ENTRYPOINT ["/container-startup.sh"]
CMD ["serve"]
