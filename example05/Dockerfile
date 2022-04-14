FROM ubuntu:20.04
WORKDIR /app
COPY cow.txt .
RUN useradd --create-home user
USER user
CMD ["/usr/bin/cat", "cow.txt"]
