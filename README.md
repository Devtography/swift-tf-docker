# Swift for TensorFlow - Docker

<img src="https://github.com/iamWing/swift-tf-docker/blob/master/images/logo.png?raw=true" alt="Swift + TensorFlow logo" >

### An Ubuntu 18.04 Docker image for [Swift for TensorFlow].

#### You can find the Docker Hub repo here: https://hub.docker.com/r/devtography/swift-tf

### Supported tags & respective Swift for TensorFlow version

| Tag           | Swift for TensorFlow |
| ------------- | -------------------- |
| 1.0.1, latest | v0.5.0 |
| 1.0.0         | v0.5.0 |

_* Append `-cuda` postfix for GPU supported images_

### Usage

##### Pull the Docker image from Docker Hub:

```bash
# CPU only
docker pull devtography/swift-tf

# With CUDA support
docker pull devtography/swift-tf:latest-cuda
```

##### Create a container from the image and run it:

```bash
docker run -it devtography/swift-tf
```

If you want to run the Swift REPL you will need to run the container with 
additional privileges:

```bash
docker run --security-opt seccomp=unconfined -it devtography/swift-tf
```

For GPU support on Linux, [install NVIDIA Docker support] and run a GPU-enabled 
Swift for TensorFlow image:

- Take note of your Docker version with `docker -v`. Versions __earlier than__
  19.03 require nvidia-docker2 and the `--runtime=nvidia` flag. On versions 
  _including and after_ 19.03, you will use the `nvidia-container-toolkit` 
  package and the `--gpus all` flag.

```bash
# Docker version >= 19.03
docker run --gpus all -it devtography/swift-tf:latest-cuda

# Docker version < 19.03
docker run --runtime=nvidia -it devtography/swift-tf:latest-cuda
```

___Note from official [Swift for TensorFlow installation doc]:___

> If you are using a CUDA build and you have an NVIDIA GPU with a compute 
  capability other than 3.5 or 7.0, then you will experience a ~10 minute delay 
  the first time you execute a TensorFlow operation, while TensorFlow compiles 
  kernels for your GPU's compute capability. The program will not print 
  anything out and it will appear to be frozen.

## Remarks

### Jupyter Notebook support

Jupyter Notebook support for Swift is __NOT__ included in the docker images. 
If you would like to try [Swift for TensorFlow] in a Jupyter Notebook, Google's 
[Colaboratory] provides a free an no setup required environment that runs 
entirely in the cloud with GPU support.

For more details, please follow the [usage] document of [Swift for TensorFlow].

## Contributions

Contributions via pull requests are welcome and encouraged :)

## License

swift-tf-docker is licensed under the [Apache License, Version 2.0](LICENSE.md).

[Swift for TensorFlow]: https://github.com/tensorflow/swift
[install NVIDIA Docker support]: https://github.com/NVIDIA/nvidia-docker
[Swift for TensorFlow installation doc]: https://github.com/tensorflow/swift/blob/master/Installation.md
[Colaboratory]: https://colab.research.google.com/
[usage]: https://github.com/tensorflow/swift/blob/master/Usage.md
