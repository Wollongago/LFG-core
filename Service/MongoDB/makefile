.PHONY: build bash

DB?=LFG

default:
	@echo "Default target"
	
build:
	@echo "============= Building MongoDB ============="
	test -n "$(VERSION)" # $$VERSION
	docker build --label lfg.mongodb.version:latest \
	-t lfg-mongodb \
	-f Dockerfile .

bash:
	@echo "============= Entering MongoDB bash shell ============="
	@docker exec -it $$(docker ps -aqf "name=lfg-mongodb-1") /bin/bash