# Seanime Docker

A simple, Docker image for [Seanime](https://seanime.rahim.app/).

Video transcoding via [FFmpeg](https://ffmpeg.org/) works out of the box.

Unlike umag's version, the server image is based on `nvidia/cuda:12.6.3-runtime-ubuntu24.04` image instead of alpine images. This is because alpine images do not support CUDA/NVENC, so hardware transcode will not work. To verify that the container has CUDA/NVENC support with FFMPEG, run `ffmpeg -hide_banner -init_hw_device "list"` and `cuda` should be an option.

## Usage

### Docker Compose

```yaml
services:
  seanime:
    image: ghcr.io/aericio/seanime-docker/seanime
    container_name: seanime
    volumes:
      - /mnt/user/anime:/anime
      - /mnt/user/downloads:/downloads
      - ./seanime-config:/root/.config/Seanime
    ports:
      - 3211:43211
    restart: always
```

## Configuration

### Ports

`3211` - Seanime web interface.


### Volumes

`/anime` - Downloads and media files are stored here.

`/seanime-config` - This is where the configuration files for Seanime are located.

`downloads` - Torrent downloads dir
