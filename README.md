# TP-Link Unified Add-ons

Home Assistant add-on repository for the TP-Link Unified project.

## Add-ons

- **TP-Link Unified Video Bridge** — runs go2rtc with native `tapo://` streams so Tapo battery/solar cameras and doorbells can show live video/audio in Home Assistant.

## Install

1. Home Assistant → Settings → Add-ons → Add-on Store.
2. Three-dot menu → Repositories.
3. Add this repository URL:

   ```text
   https://github.com/c0r391/tplink-unified-video-addon
   ```

4. Install **TP-Link Unified Video Bridge**.
5. Configure each camera.
6. Start the add-on.
7. Add the same camera in the TP-Link Unified HACS integration.

## Camera options

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

## Support this project

If this add-on is useful for your dashboard or automation setup, BTC support is appreciated and helps keep the project maintained.

```text
bc1qqe5l9e36h49wm9kkjrek7v746gej3s3j2hrkgd
```

## Credits

Built on top of [go2rtc](https://github.com/AlexxIT/go2rtc). This repository provides an independent Home Assistant add-on and is not affiliated with TP-Link or go2rtc.
