.PHONY: build bash

default:
	@echo "Default target"

build:
	@echo "============= Building Redis ============="
	test -n "$(VERSION)"  # $$VERSION
	docker build --label lfg.redis.version=${VERSION} \
	-t lfg-redis:${VERSION} \
	-t lfg-redis:latest \
	-f Dockerfile .

push:
	@echo "============= Pushing Redis image into the repo ============="
	test -n "$(VERSION)"  # $$VERSION
	docker push lfg-redis:latest && \
    docker push lfg-redis:${VERSION}

bash:
	@echo "============= Entering Redis bash shell ============="
	@docker exec -it $$(docker ps -aqf "name=lfg-redis-1") /bin/sh
