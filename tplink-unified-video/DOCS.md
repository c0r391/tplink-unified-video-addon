# TP-Link Unified Video Bridge documentation

## Quick start

1. Install the add-on.
2. Open Configuration.
3. Add one entry per TP-Link/Tapo camera, or let a compatible integration configure streams automatically:

```yaml
log_level: info
cameras:
  - name: cam_192_0_2_10
    host: 192.0.2.10
    username: admin
    password: your-tapo-password
```

4. Start the add-on.
5. Open the add-on log and confirm it starts go2rtc.
6. Add the camera in the TP-Link Unified integration.

EOOEIES cameras use the separate `eooeies_cameras` option and are normally written by the EOOEIES integration through the Supervisor API:

```yaml
log_level: info
eooeies_cameras:
  - name: eooeies_front_live
    source: http://<home-assistant-host>/api/eooeies_cloud/live/<entry_id>/<serial>.h264
```

`cameras` and `eooeies_cameras` are merged independently. Updating one provider must not remove the other provider's streams.

## TP-Link/Tapo naming

The TP-Link Unified integration currently expects:

```text
cam_<camera_ip_with_underscores>_hd
```

For camera `192.0.2.10`, use:

```yaml
name: cam_192_0_2_10
```

The add-on creates:

```text
cam_192_0_2_10_hd
cam_192_0_2_10_sd
```

## EOOEIES naming

For EOOEIES, the `name` is used directly as the go2rtc stream name. The EOOEIES integration uses names like:

```text
eooeies_eingang_live
eooeies_oben_live
```

## Which password?

Use `username: admin`.

For many newer Tapo battery/solar cameras, the mobile app does **not** show a separate Camera Account/RTSP/ONVIF password. Use the same Tapo/TP-Link password that you entered in TP-Link Unified for that camera. This is the validated path for TC82/C410-style cameras in the Test-HA setup.

If your camera/app does show a separate Camera Account, use that camera-specific password instead.

## Security

Passwords are read from Home Assistant add-on options and only a SHA-256 hash is written into the generated go2rtc config. The add-on does not print TP-Link/Tapo source URLs. EOOEIES sources should point to local Home Assistant raw-H264 bridge endpoints, not contain EOOEIES account credentials.
