TAG=2.10.0-beta2-scratch

build:
	DOCKER_BUILDKIT=1 docker build -t skillc0der/tarantool:$(TAG) .

login:
	docker login

push: build login
	docker push skillc0der/tarantool:$(TAG)

build-base:
	DOCKER_BUILDKIT=1 docker build --target base -t tar-base .

debug: build-base
	docker run --rm -it tar-base ash

.PHONY: build login push build-base debug
