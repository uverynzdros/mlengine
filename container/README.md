# Chainer on Cloud ML Engine

## Build

```shell
PROJECT_ID=$(gcloud config list project --format "value(core.project)")
IMAGE_REPO_NAME=chainer_custom_container
IMAGE_TAG=cifar10_gpu
IMAGE_URI=gcr.io/$PROJECT_ID/$IMAGE_REPO_NAME:$IMAGE_TAG
docker build -f chainer/Dockerfile -t $IMAGE_URI ./
gcloud auth configure-docker
docker push $IMAGE_URI
```

## Submit job

```shell
PROJECT_ID=$(gcloud config list project --format "value(core.project)")
IMAGE_REPO_NAME=chainer_custom_container
IMAGE_TAG=cifar10_gpu
IMAGE_URI=gcr.io/$PROJECT_ID/$IMAGE_REPO_NAME:$IMAGE_TAG
JOB_NAME=custom_container_job_001
REGION=us-central1
gcloud beta ml-engine jobs submit training $JOB_NAME \
  --scale-tier BASIC_GPU \
  --region $REGION \
  --master-image-uri $IMAGE_URI \
  -- \
  --gpu 1 \
  --dataset 'cifar10'
```
