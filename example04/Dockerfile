FROM ubuntu:20.04
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
&& apt-get install --yes --no-install-recommends cowsay=3.03+dfsg2-7 \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& useradd --create-home user

USER user

CMD ["/usr/games/cowsay", "hello"]
