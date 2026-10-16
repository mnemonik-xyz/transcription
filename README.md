# Transcription worker

GPU and CPU container images for the authenticated `faster-whisper` HTTP transcription service.
It exposes `GET /health`, `POST /job`, `GET /job/<job_id>`, and `GET /jobs` on port `8080`.

Set a random `WARRANT_WORKER_TOKEN` of at least 32 characters before starting the container. Uploads
require a bearer token, `Content-Length`, and an `X-Audio-SHA256` checksum.

## Images

GitHub Actions publishes `ghcr.io/mnemonik-xyz/transcription:<tag>` as a multi-architecture
manifest: Linux amd64 resolves to the CUDA image and Linux arm64 to the CPU image. The explicit
variants remain available as `:<tag>-amd64` and `:<tag>-arm64`. Release tags publish automatically;
`workflow_dispatch` can publish a named operational tag such as `pilot`.

## Local checks

```sh
python3 -m unittest -v
ruff check .
```

## Local image build

```sh
docker build -t transcription:dev .
docker build -f Dockerfile.arm64 -t transcription:dev-arm64 .
```
