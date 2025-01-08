<!-- DO NOT EDIT THIS FILE MANUALLY -->
<!-- Please read https://github.com/imagegenius/docker-immich/blob/main/.github/CONTRIBUTING.md -->

Immich is a high performance self-hosted photo and video backup solution.

[![immich](https://raw.githubusercontent.com/immich-app/immich/main/design/immich-logo-inline-dark.png)](https://immich.app/)

## Supported Architectures

We use Docker manifest for cross-platform compatibility. More details can be found on [Docker's website](https://distribution.github.io/distribution/spec/manifest-v2-2/#manifest-list).

This image supports the following architectures:

| Architecture | Available | Tag |
| :----: | :----: | ---- |
| x86-64 | ✅ | amd64-\<version tag\> |
| arm64 | ✅ | arm64v8-\<version tag\> |
| armhf | ❌ | |

## Version Tags

This image offers different versions via tags. Be cautious when using unstable or development tags, and read their descriptions carefully.

| Tag | Available | Description |
| :----: | :----: |--- |
| latest | ✅ | Latest Immich release. |
| noml | ✅ | Latest Immich release. Machine-learning is completely removed. |
| cuda | ✅ | Latest Immich release. Machine-learning supports cuda (Nvidia). |
| openvino | ✅ | Latest Immich release. Machine-learning supports openvino (Intel). |
| armnn | ✅ | Latest Immich release. Machine-learning supports ARM board. |

## Application Setup

Access the WebUI at `http://your-ip:2283`. Follow the setup wizard to configure Immich.
### Requirements

- **PostgreSQL**:  setup internally inside the stack.
- **Redis**: setup internally inside the stack.

### Intel Hardware Acceleration

To enable Intel Quicksync:

1. Ensure container access to `/dev/dri`.
2. Add `/dev/dri` to your Docker run command:

   ```bash
   docker run --device=/dev/dri:/dev/dri ...
   ```

To enable OpenVINO:

1. Make sure your [CPU supports OpenVINO](https://docs.openvino.ai/2024/about-openvino/system-requirements.html)
2. Add `--device-cgroup-rule='c 189:* rmw'` and  `-v /dev/bus/usb:/dev/bus/usb` to your Docker run command:

   ```bash
   docker run --device=/dev/dri --device-cgroup-rule='c 189:* rmw' -v /dev/bus/usb:/dev/bus/usb ...
   ```

### Nvidia Hardware Acceleration

1. Install the Nvidia container runtime as per [these instructions](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html).

2. Create a new Docker container using the Nvidia runtime:

   - Use `--runtime=nvidia` and `NVIDIA_VISIBLE_DEVICES=all` in your Docker run command, or specify a particular GPU UUID instead of `all`.

   ```bash
   docker run --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=all
   ```

   - Alternatively, use `--gpus=all` to enable all GPUs.

   ```bash
   docker run --gpus=all ...
   ```
### ARMNN Hardware Acceleration

1. Using the `hwaccel.ml.yml`

2. Or add into the docker-compose

   ```bash
       devices:
      - /dev/mali0:/dev/mali0
    volumes:
      - /lib/firmware/mali_csffw.bin:/lib/firmware/mali_csffw.bin:ro # Mali firmware for your chipset (not always required depending on the driver)
      - /usr/lib/aarch64-linux-gnu/libmali.so.1.9.0:/usr/lib/libmali.so:ro # Mali driver for your chipset (always required)
   ```

## Usage

1. Clone the github 
   ```bash
   git clone https://github.com/thanhtantran/docker-immich
   cd docker-immich
   ```
2. Start the container
  ```bash
   docker compose up -d
   ```


### Docker Compose



## Versions


