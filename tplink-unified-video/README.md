# TP-Link Unified Video Bridge

Runs [go2rtc](https://github.com/AlexxIT/go2rtc) as the shared video bridge for TP-Link Unified and compatible EOOEIES Home Assistant integrations.

This add-on is the easy path for non-technical users: install once, let integrations configure camera streams, start. No Docker commands and no hand-written go2rtc YAML.

## Why this add-on exists

Many Tapo battery/solar cameras and doorbells do not expose normal RTSP on port 554. EOOEIES cameras also need a bridge from their cloud/WebRTC live path into Home Assistant media streams. This add-on keeps both provider types in one go2rtc instance and provides:

- RTSP for Home Assistant's `stream` integration.
- JPEG frames for snapshots.
- WebRTC support where clients use it.
- Audio when the camera stream exposes it.

## TP-Link/Tapo options

```yaml
log_level: info
cameras:
  - name: front_door
    host: 192.0.2.10
    username: admin
    password: your-tapo-password
```

Use `username: admin`. For newer Tapo battery/solar cameras the Tapo app may not show a separate **Camera Account** page. In that case, use the same Tapo/TP-Link password that you use when adding the camera to the TP-Link Unified integration. The add-on hashes this password into the `tapo://admin:<SHA256>@...` format expected by go2rtc.

If your Tapo app does expose a separate **Camera Account / RTSP / ONVIF** password, use that password instead.

The add-on automatically hashes the password as required by go2rtc's Tapo source URL. The generated URL is not printed in logs.

## EOOEIES options

EOOEIES cameras are normally added automatically by the EOOEIES integration. Advanced users can provide raw-H264 bridge sources manually:

```yaml
log_level: info
eooeies_cameras:
  - name: eooeies_front_live
    source: http://<home-assistant-host>/api/eooeies_cloud/live/<entry_id>/<serial>.h264
```

The add-on keeps `cameras` and `eooeies_cameras` separate, so TP-Link/Tapo streams continue to run when EOOEIES streams are added, and EOOEIES streams continue to run when TP-Link/Tapo cameras are updated.

## Streams created

For each TP-Link/Tapo camera, two streams are created:

- `<name>_hd` → subtype `0`
- `<name>_sd` → subtype `1`

Example:

```text
front_door_hd
front_door_sd
```

TP-Link Unified uses stream names of the form `cam_<ip_with_underscores>_hd` by default, so for lowest-effort setup set the add-on camera name to e.g.:

```text
cam_192_0_2_10
```

Each EOOEIES camera creates exactly the stream name provided in `eooeies_cameras[].name`, for example:

```text
eooeies_front_live
```

## Health check

Open:

```text
http://<home-assistant-ip>:1984
```

or check that:

```text
http://<home-assistant-ip>:1984/api/schemes
```

contains `tapo`.
