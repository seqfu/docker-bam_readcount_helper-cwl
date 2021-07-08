NAME   := seqfu/alpine-bam_readcount
IMG    := ${NAME}
LATEST := ${NAME}
HOST   := $$(basename ${NAME})
PWD    := $$(pwd)

build:
	@docker build -f Dockerfile -t ${IMG} .
	@docker tag ${IMG} ${LATEST}
 
push:
	@docker push ${NAME}

run:
	docker run --rm --hostname ${HOST} ${LATEST} bam-readcount

interact:
	docker run --rm --hostname ${HOST} --detach-keys="ctrl-@" -t -i ${LATEST} /bin/bash

login:
	@docker log -u ${DOCKER_USER} -p ${DOCKER_PASS}
