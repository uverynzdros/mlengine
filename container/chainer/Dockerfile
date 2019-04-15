FROM chainer/chainer

COPY cifar10/ /chainer/cifar10/
COPY training.py /chainer

WORKDIR /chainer

ENTRYPOINT [ "python", "/chainer/training.py" ]
