NAME=guillaumelecerf/deb-package-builder
TAG=ubuntu-xenial

all:
	docker build --force-rm -t $(NAME):$(TAG) .

nocache:
	docker build --force-rm --no-cache -t $(NAME):$(TAG) .
