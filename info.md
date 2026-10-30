{% if prerelease %}
### NB!: This is a Beta release!
{% endif %}

[![GitHub Release][releases-shield]][releases]
[![License][license-shield]][license]
[![Community Forum][forum-shield]][forum]

Home Assistant custom integration for **Beward** surveillance devices and doorbells.

*Maintained fork with support for **DS91406M** and newer firmware profiles.*

![Beward Logo][exampleimg]

## Key Features

- **Live Video Streaming:** High-quality H.264 video feed delivered over RTSP.
- **Still Image Snapshots:** Real-time JPEG snapshots fetched directly via camera CGI.
- **Doorbell Press Sensor (`Ding`):** Instant binary sensor updates on visitor calls.
- **Connectivity Sensor:** Continuous device reachability tracking.
- **Visitor Snapshots:** Automated caching of visitor photos during call button events.

{% if not installed %}
## Setup Instructions

1. Click **Download** to install the custom component files.
2. Restart Home Assistant Core.
3. In Home Assistant, go to **Settings** -> **Devices & Services** -> **Add Integration**.
4. Search for **Beward** and enter your device IP address and credentials.
{% endif %}

## Authors & Acknowledgments

- **Original Project:** Developed by [Andrey "Limych" Khrolenok](https://github.com/Limych).
- **Fork Updates & Intercom Extensions:** [Sergey Zazhigaev](https://github.com/zazhigaev).

Distributed under the **MIT License**.

[releases-shield]: https://img.shields.io/github/release/zazhigaev/ha-beward.svg?style=popout
[releases]: https://github.com/zazhigaev/ha-beward/releases
[license-shield]: https://img.shields.io/badge/license-MIT-blue.svg?style=popout
[license]: https://github.com/zazhigaev/ha-beward/blob/master/LICENSE.md
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg?style=popout
[forum]: https://community.home-assistant.io/t/beward-cameras-and-doorbells-integration/129388
[exampleimg]: https://github.com/zazhigaev/ha-beward/raw/master/beward.png
