FROM bcgovimages/von-image:py36-1.16-1

USER root

RUN mkdir -p /acapy-mediator
WORKDIR /acapy-mediator

ADD https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 /usr/bin/jq
RUN chmod +x /usr/bin/jq

USER $user

COPY requirements-latest.txt ./

RUN pip install -r ./requirements-latest.txt

# Copy the necessary files from the mediator sub-folder
COPY start.sh start.sh
RUN chmod +x start.sh
COPY configs configs

RUN aca-py --version > ./acapy-version.txt

ENTRYPOINT ["bash", "./start.sh"]
