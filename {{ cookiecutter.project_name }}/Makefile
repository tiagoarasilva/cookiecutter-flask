.DEFAULT_GOAL := help

.PHONY: help
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

.PHONY: clean
clean: clean_pyc ## Clean all PYC in the system

.PHONY: clean_pyc
clean_pyc: ## Cleans all *.pyc in the system
	find . -type f -name "*.pyc" -delete || true

.PHONY: requirements
requirements: ## Installs the dev requirements
	pip install -r requirements/requirements-dev.txt

.PHONY: docker
docker: ## Styarts the docker compose
	docker-compose up

.PHONY: docker-no-log
docker-no-logs: ##  Starts the docker compose without stdout logs
	docker-compose up -d

.PHONY: docker-stop
docker-stop: ## Stops the docker containers
	docker-compose stop

.PHONY: run-local
run-local: ## Starts the local server
	python -m src.serve

.PHONY: run-special
run-special: ## Starts the server by passing a special settings file `FLASK_SETTINGS_FILENAME`
	FLASK_SETTINGS_FILENAME=$(FLASK_SETTINGS_FILENAME) python -m src.serve

.PHONY: test
test: ## Runs the local tests
	pytest

.PHONY: mypy
mypy: ## Runs the typing analyser
	mypy src/

ifndef VERBOSE
.SILENT:
endif
