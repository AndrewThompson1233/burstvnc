# BurstVNC

Low-latency remote desktop streaming engine with client-side cursor decoupling and hardware-accelerated video pipelines.

## Capabilities

- Hardware-decoupled cursor: cursor rendered locally in browser or native client at monitor refresh rate (120/144/240 Hz).
- Tactile feedback: local click ripple before round-trip acknowledgement.
- Multi-backend encoding: NVENC (Turing/Ampere), VAAPI, and CPU libx264 with AVX2.
- Pointer lock: raw delta motion input for 3D navigation and games.
- Periodic Intra-Refresh (PIR): avoids full-frame IDR bitrate spikes over lossy networks.
- Dual client: WebCodecs hardware decode in browser, SDL2 client in C++.

## Build

```bash
mkdir -p build && cd build
cmake .. -GNinja
ninja
```

## Run

Start the server:

```bash
./build/burst_srv --display :99 --port 8080 --fps 60 --bitrate 8000
```

With hardware acceleration:

```bash
./build/burst_srv --display :99 --port 8080 --fps 120 --bitrate 12000 --encoder nvenc
```

CPU fallback:

```bash
./build/burst_srv --display :99 --port 8080 --fps 60 --bitrate 6000 --encoder x264
```

## Connect

- Web: `http://<HOST>:8080/`
- Native client: `./build/burst_cli <HOST> 8080`
