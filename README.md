# ECMREC Retail README

[English](README.md) | [繁體中文](README.zh-TW.md)

ECMREC is a Windows-focused camera application for live preview, snapshots, continuous segmented MP4 recording, remote control, camera-disconnect recovery, and local event logging. Preview and recording require a compatible Transcend ECM100 camera.

<a id="toc"></a>
## Contents

- [Compatibility](#compatibility)
- [Hardware Requirements](#hardware-requirements)
- [EXE Runtime Required Files](#exe-runtime-required-files)
- [Product Binding Requirement](#product-binding-requirement)
- [Overview](#overview)
- [Main Features](#features)
- [Product Positioning](#positioning)

<a id="compatibility"></a>
## Compatibility

- Transcend ECM100 (mandatory)

[Back to Contents](#toc)

<a id="hardware-requirements"></a>
## Hardware Requirements

1. **Supported Platforms**

- Windows 10/11 x64

2. **CPU Recommendation**

- At least 4 CPU cores is recommended.
- 8 cores / 16 threads can run this application stably.

3. **RAM Recommendation**

- At least 16 GB RAM is recommended.

[Back to Contents](#toc)

<a id="exe-runtime-required-files"></a>
## EXE Runtime Required Files

Current packaged folder structure:

```text
ECM100REC/
	ECM100REC.exe
	config.ini
	FFmpeg/
		ffmpeg.exe
	_internal/
		... (Python runtime and packaged dependencies)
	<HOSTNAME>/
		ecm100rec.db
```

Required to run:

- `ECM100REC.exe`
- `FFmpeg/ffmpeg.exe`
- `_internal/`

Usually keep with distribution:

- `config.ini` (runtime settings file)

Runtime-generated data (not required for a fresh package):

- `<HOSTNAME>/` and `ecm100rec.db`

[Back to Contents](#toc)

<a id="product-binding-requirement"></a>
## Product Binding Requirement

This software requires an ECM100 device to use preview and recording features. The application enforces this at runtime:

- Preview start is blocked when no device name containing `ECM100` is detected.
- Recording start is blocked when no device name containing `ECM100` is detected.
- If an ECM error is raised during preview/record start checks, the current preview stream is stopped immediately.

[Back to Contents](#toc)

<a id="overview"></a>
## Overview

ECM100REC is a Windows-focused camera recording tool with the following core capabilities:

- Live camera preview and resolution switching.
- Continuous segmented recording to MP4 files.
- Optional timestamp overlay on recorded frames.
- Local SQLite logging for commands, recordings, and camera events.
- Windows startup integration.

[Back to Contents](#toc)

<a id="features"></a>
## Main Features

### 1. Live preview and device management

- Scans available camera devices.
- Requires at least one camera whose device name contains `ECM100`.
- Supports resolution switching.
- Displays HUD status, FPS, and current output file name.
- The preview crosshair can be toggled on and off from the UI.

### 2. Recording and timestamp overlay

- Uses FFmpeg to write MP4 files.
- Supports continuous segmented recording.
- Can overlay timestamps on recorded frames.
- On Windows, the default codec choices are `h264_qsv`, `libx264`, and `hevc_qsv`.
- Recording now warns when the target storage space is getting low, and automatically stops when the storage threshold is reached.
- Low-space warning threshold, hard-stop threshold, and disk check interval are configurable in `config.ini`.
- Manual stop actions now require confirmation before ending an active recording.

### 3. Recording continuity and recovery

- Maintains segmented recording flow over long sessions.
- Includes camera disconnect handling and reconnection flow.
- Supports safe stop behavior when reconnection is skipped.
- Status messages use stronger severity styling so warnings and errors are easier to notice.
- After camera reconnect or preview recovery, the UI shows clearer stop/reconnect status text.

### 4. SQLite activity logging

When SQLite is enabled, the application creates or maintains tables for:

- Recording start and stop commands
- Video recording records
- External file paths received through SAVE commands
- Camera disconnect and related events

### 5. Persistent settings and auto-start

- Stores save path, duration, timestamp, quality, and codec values in `config.ini`.
- Supports Windows startup registration.
- Generates a device UUID on first run.

[Back to Contents](#toc)

<a id="positioning"></a>
## Product Positioning

ECM100REC is designed for camera-based recording workflows that need:

- Stable long-running segmented recording.
- Lightweight local operation.
- A simple operator UI with centralized control of device, quality, and recording behavior.

[Back to Contents](#toc)
