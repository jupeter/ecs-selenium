VERSION=3.14.0
REGION=us-west-2
ACCOUNT_ID=111122223333
REGISTRY=$(ACCOUNT_ID).dkr.ecr.$(REGION).amazonaws.com
IMAGE_NAME=ecs-node-chrome

clean:
	rm -rf common

build:
	mkdir -p common/
	rsync -av ../common/* common/
	docker build -t $(IMAGE_NAME) --build-arg VERSION=$(VERSION) .
	rm -rf common/

tag: build
	docker tag $(IMAGE_NAME) $(REGISTRY)/$(IMAGE_NAME):$(VERSION)
	docker tag $(IMAGE_NAME) $(REGISTRY)/$(IMAGE_NAME):latest

push: tag
	docker push $(REGISTRY)/$(IMAGE_NAME):$(VERSION)
	docker push $(REGISTRY)/$(IMAGE_NAME):latest
