# TP-Link Unified Add-ons

Home Assistant add-on repository for the TP-Link Unified project and shared camera live-video bridge.

## Add-ons

- **TP-Link Unified Video Bridge** — runs go2rtc for TP-Link/Tapo `tapo://` streams and EOOEIES raw-H264 bridge sources, so both integrations can share one Home Assistant add-on for live video/audio where supported.

## Install

1. Home Assistant → Settings → Add-ons → Add-on Store.
2. Three-dot menu → Repositories.
3. Add this repository URL:

   ```text
   https://github.com/c0r391/tplink-unified-video-addon
   ```

4. Install **TP-Link Unified Video Bridge**.
5. Start the add-on.
6. Add cameras in a compatible Home Assistant integration. TP-Link Unified and EOOEIES Cloud can configure this add-on automatically through the Supervisor API.

## Normal configuration path

You usually do **not** need to edit the YAML below. Install and start the add-on, then add cameras in the integration UI:

- **TP-Link Unified** writes TP-Link/Tapo `cameras` options.
- **EOOEIES Cloud** writes EOOEIES `eooeies_cameras` options.

The manual options are documented only for diagnostics and advanced setups.

## Advanced/manual TP-Link/Tapo camera options

Use `username: admin`. If the Tapo app does not show a separate Camera Account page, use the same Tapo/TP-Link password used in TP-Link Unified. If your camera/app exposes a separate Camera Account/RTSP/ONVIF password, use that camera-specific password instead.

```yaml
log_level: info
cameras:
  - name: cam_192_0_2_10
    host: 192.0.2.10
    username: admin
    password: your-tapo-password
```

The add-on generates the SHA-256 password hash required by go2rtc and does not print source URLs in logs.

## Advanced/manual EOOEIES camera options

EOOEIES support is intended to be configured automatically by the EOOEIES Home Assistant integration. Manual options are available for diagnostics or advanced setups:

```yaml
log_level: info
eooeies_cameras:
  - name: eooeies_front_live
    source: http://<home-assistant-host>/api/eooeies_cloud/live/<entry_id>/<serial>.h264
```

The add-on preserves TP-Link/Tapo `cameras` and EOOEIES `eooeies_cameras` independently so installing or updating one integration does not remove the other provider's streams.

## Support this project

If this add-on is useful for your dashboard or automation setup, BTC support is appreciated and helps keep the project maintained.

```text
bc1qqe5l9e36h49wm9kkjrek7v746gej3s3j2hrkgd
```

## Credits

Built on top of [go2rtc](https://github.com/AlexxIT/go2rtc). This repository provides an independent Home Assistant add-on and is not affiliated with TP-Link or go2rtc.
