.PHONY: build up down shutdown logs test clear stop

I ?= default
export UID:=$(shell id -u)
export GID:=$(shell id -g)

default:
	@echo "Default target"

build:
	@echo "============= Building Celery ============="
	test -n "$(VERSION)" # $$VERSION
	docker build --label lfg.celery.version=${VERSION} \
	-t lfg-celery:${VERSION} \
	-t lfg-celery:latest \
	-f Dockerfile .

push:
	@echo "============= Pushing Celery image into the repo ============="
	test -n "$(VERSION)"  # $$VERSION
	docker push lfg-celery:latest && \
    docker push lfg-celery:${VERSION}

up:
	@echo "============= Sarting Celery Instances ============="
	@docker network inspect lfg-net >/dev/null || docker network create -d bridge --subnet 42.42.0.0/24 --gateway 42.42.0.1 lfg-net
	docker-compose -p lfg up -d

down:
	@echo "============= Shutdown Everything ============="
	docker-compose -p lfg down --remove-orphans

restart:
	@echo "============= Restart Celery: $(I) ============="
	@LOGPATH=$$(docker inspect --format='{{.LogPath}}' lfg-celery-$(I)-1); \
	if [ -n "$${LOGPATH}" ]; then sudo truncate -s 0 $${LOGPATH}; fi
	docker-compose -p lfg restart celery-$(I)

stop:
	@echo "============= Stopping Celery: $(I) ============="
	docker-compose -p lfg stop celery-${I}

logs:
	@echo "============= Logs of Celery: $(I) ============="
	docker-compose -p lfg logs -f celery-${I}

bash:
	@echo "============= Entering Celery bash shell as $(UID):$(GID) ============="
	@docker exec --user $(UID):$(GID) -it $$(docker ps -aqf "name=lfg-celery-$(I)-1") /bin/bash

# How to lowercase
# @LOWER_I=$$(echo '${I}' | tr '[:upper:]' '[:lower:]'); echo "$${LOWER_I}"; \
# if [ -n "$${LOWER_I}" ]; then docker-compose -p lfg logs -f celery-$${LOWER_I}; else echo "please define celery instance"; fi
