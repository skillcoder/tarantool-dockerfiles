TAG=2.10.0-beta2-queue

build:
	DOCKER_BUILDKIT=1 docker build -t skillc0der/tarantool:$(TAG) .

login:
	docker login

push: login
	docker push skillc0der/tarantool:$(TAG)

.PHONY: build login push
