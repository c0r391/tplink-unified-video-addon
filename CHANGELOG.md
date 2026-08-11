# Changelog

## 0.1.1 - Fix Home Assistant add-on build metadata

- Move Home Assistant base-image build metadata into `build.yaml` so the add-on builder sets `BUILD_FROM` correctly.
- Keep `config.yaml` focused on add-on runtime metadata/options.

## 0.1.0 - Initial public alpha

- Add TP-Link Unified Video Bridge Home Assistant add-on.
- Run go2rtc with native `tapo://` support.
- Generate HD/SD Tapo stream config from simple add-on options.
- Avoid logging generated source URLs or password hashes.
