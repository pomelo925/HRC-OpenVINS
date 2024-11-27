# HRC Lab - OpenVINS Learning

> Learning initiated on 2024/11/22
> Open-VINS official github: https://github.com/rpng/open_vins.git

This repository is part of HRC Lab's initiative to study Open-VINS.

The primary focus is on:

* Restructurt the Open-VINS Docker environment.
* Evaluate the algorithm's performance and efficiency.

## Usage 

1. Clone this repository.
    ```=
    git clone https://github.com/pomelo925/HRC-OpenVINS
    ```

2. Launch Docker Container.
    ```=
    cd HRC-OpenVINS.docker
    ./exp.sh
    ```

## Call Out

1. [Official Dockerfile](https://github.com/rpng/open_vins/blob/master/Dockerfile_ros2_22_04) 做工粗糙，完全沒做容量優化。

2. Workspace 編譯工作量巨大，建議編譯使用 `--parallel-workers` 管理、container 使用 `deploy: limits` 參數。

3. 注意編譯生成文件 `.o` & `.so` 容量巨大，須由 Git LFS 管理。 

4. 官方尚未提供 binary package。

5. ROS1/2 Bag Download Gateway Error。