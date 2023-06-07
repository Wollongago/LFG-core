.PHONY: build

default:
	@echo "Default target"

build:
	@echo "============= Building RabbitMQ ============="
	test -n "$(VERSION)"  # $$VERSION
	docker build --label lfg.rabbitmq.version:${VERSION} \
	-t lfg-rabbitmq:${VERSION} \
	-t lfg-rabbitmq:latest \
	-f Dockerfile .
