# TP-Link Unified Video Bridge documentation

## Quick start

1. Install and start the add-on.
2. Add cameras in a compatible Home Assistant integration.
3. Let the integration configure this add-on automatically through the Supervisor API.

Manual YAML is only for diagnostics or advanced setups.

## Advanced/manual TP-Link/Tapo options

```yaml
log_level: info
cameras:
  - name: cam_192_0_2_10
    host: 192.0.2.10
    username: admin
    password: your-tapo-password
```

After changing manual options, restart the add-on and check the log to confirm it starts go2rtc.

## Advanced/manual EOOEIES options

EOOEIES cameras use the separate `eooeies_cameras` option and are normally written by the EOOEIES integration through the Supervisor API. Manual entries are only for diagnostics:

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
