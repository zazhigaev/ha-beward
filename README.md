# ha-beward

[![GitHub Release][releases-shield]][releases]
[![GitHub Activity][commits-shield]][commits]
[![License][license-shield]][license]
[![hacs][hacs-shield]][hacs]
[![Maintainer][maintenance-shield]][user_profile]
[![Community Forum][forum-shield]][forum]

Home Assistant custom component for integrating **Beward** video intercoms, doorbells, and IP cameras.

This repository is a maintained fork of the original [ha-beward integration by Limych][original-component], extended with support for newer intercom hardware (including the **DS91406M** series) and bundled with an updated [`py-beward`][py-beward-repo] backend library.

![Beward Logo][exampleimg]

---

## Supported Features

- **Live RTSP Stream & Snapshots:** View high-resolution video streams and retrieve still images via HTTP CGI.
- **Doorbell Call Sensor:** Immediate detection of physical call button presses (`SensorAlarm`).
- **Device Availability Sensor:** Real-time online/offline connectivity monitoring.
- **Visitor & Motion History:** Access timestamps and captured frames of the last doorbell press and motion events.

---

## Supported Device Types & Models

There is currently support for the following device types within Home Assistant:
- [Binary Sensor](#binary-sensor)
- [Camera](#camera)
- [Sensor](#sensor)

---

### Binary Sensor

Binary sensor entities reflect hardware state transitions:

- **Online (`DeviceOnline`):** Reports device availability in the local network (all models).
- **Ding / Call (`SensorAlarm`):** Reports physical call button presses (doorbell models only).

#### Supported Doorbell Models:
- ALP-600, DC11EP, DK103, DK103M, DKS20210
- DS03M, DS05M(P), DS06, DS06M, DS06A(P), DS07P-LP
- DSN06PS, DSN23215PS
- **DS91406M** *(Added in this fork)*
- S06A, S06M

---

### Camera

Exposes video feeds and snapshot mechanisms:

- **Live Stream:** Real-time H.264 video feed delivered over RTSP (`/av0_0` or secondary profiles).
- **Snapshot:** Still JPEG images fetched via HTTP CGI (`images_cgi?channel=0`).

#### Supported Models:
- **IP Cameras:** B102S (and compatible models).
- **Doorbells:** All models listed in the Doorbell section above (including DS91406M).

---

### Sensor

Provides telemetry, operational status, and historical event timestamps:

- **Last Ding:** Timestamp and snapshot of the last call button press.
- **Last Motion:** Timestamp and snapshot of the last detected motion event.
- **Last Activity:** Combined timestamp of any recent device interaction.

---

## Installation

### Method 1: Via HACS (Recommended)

1. Make sure [HACS][hacs] is installed and working in your Home Assistant instance.
2. In HACS, go to **Integrations** -> click the three dots in the top right corner -> **Custom repositories**.
3. Add repository URL: `https://github.com/zazhigaev/ha-beward` with category **Integration**.
4. Search for **Beward**, click **Download**, and select the latest release.
5. Restart Home Assistant Core.

### Method 2: Manual Installation

1. Open your Home Assistant configuration directory (where `configuration.yaml` is located).
2. If `custom_components` does not exist, create it.
3. Download the `beward.zip` archive from the [Latest Releases][releases-latest] page.
4. Extract the `beward` folder into `custom_components/`.
5. Restart Home Assistant Core.

---

## Configuration

### Via User Interface (Recommended)

1. In Home Assistant, navigate to **Settings** -> **Devices & Services** -> **Integrations**.
2. Click **+ Add Integration** and search for **Beward**.
3. Fill in the connection form:
   - **Host:** IP address of your Beward device (e.g., `192.168.0.99`)
   - **Port:** `80` (default)
   - **Username:** `admin` (or your configured username)
   - **Password:** device password
4. Click **Submit**.

### Via `configuration.yaml` (Legacy)

```yaml
beward:
  - host: 192.168.0.99
    username: YOUR_USERNAME
    password: YOUR_PASSWORD
    name: "Front Door"
```

---

## Automation Example: Send Snapshot to Telegram on Call

When someone rings the doorbell, Home Assistant can instantly send the captured image to Telegram:

```yaml
homeassistant:
  allowlist_external_dirs:
    - /config/.storage/beward

automation:
  - alias: "Front Door Ding Notification"
    trigger:
      platform: state
      entity_id: binary_sensor.front_door_ding
      to: 'on'
    action:
      - service: notify.telegram
        data:
          message: "Someone is at the door!"
          data:
            photo:
              file: /config/.storage/beward/front_door_last_ding.jpg
              caption: "Visitor at the front door"
```

---

## Troubleshooting

To enable verbose debug logging, add the following to your `configuration.yaml`:

```yaml
logger:
  default: info
  logs:
    custom_components.beward: debug
    beward: debug
```

Check the logs under **Settings** -> **System** -> **Logs**.

---

## Credits & License

- **Original Author & Maintainer:** [Andrey "Limych" Khrolenok](https://github.com/Limych) (author of the original `ha-beward` and `py-beward` implementations).
- **Fork Maintainer:** [Sergey Zazhigaev](https://github.com/zazhigaev) (DS91406M hardware integration and modern HA compatibility updates).

This project is open-source software licensed under the terms of the **MIT License**. See the [LICENSE.md](LICENSE.md) file for full details.

[original-component]: https://github.com/Limych/ha-beward
[py-beward-repo]: https://github.com/zazhigaev/py-beward
[commits-shield]: https://img.shields.io/github/commit-activity/y/zazhigaev/ha-beward.svg?style=popout
[commits]: https://github.com/zazhigaev/ha-beward/commits/master
[hacs-shield]: https://img.shields.io/badge/HACS-Custom-orange.svg?style=popout
[hacs]: https://hacs.xyz
[exampleimg]: https://github.com/zazhigaev/ha-beward/raw/master/beward.png
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg?style=popout
[forum]: https://community.home-assistant.io/t/beward-cameras-and-doorbells-integration/129388
[license]: https://github.com/zazhigaev/ha-beward/blob/master/LICENSE.md
[license-shield]: https://img.shields.io/badge/license-MIT-blue.svg?style=popout
[maintenance-shield]: https://img.shields.io/badge/maintainer-Sergey%20Zazhigaev-blue.svg?style=popout
[releases-shield]: https://img.shields.io/github/release/zazhigaev/ha-beward.svg?style=popout
[releases]: https://github.com/zazhigaev/ha-beward/releases
[releases-latest]: https://github.com/zazhigaev/ha-beward/releases/latest
[user_profile]: https://github.com/zazhigaev
[report_bug]: https://github.com/zazhigaev/ha-beward/issues/new
