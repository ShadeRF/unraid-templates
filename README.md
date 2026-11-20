# Filmhound & Recordhound for Unraid

Self-hosted recommendation apps for Plex. Both build picks from **your own library and history**, show **why** each one was picked, and never download anything on their own.

| | | |
|---|---|---|
| <img src="icons/filmhound.png" width="72"> | **[Filmhound](docs/filmhound.md)** | Movies and TV. Works with Seerr, Radarr, Sonarr, Letterboxd and Trakt. Port 8788. |
| <img src="icons/recordhound.png" width="72"> | **[Recordhound](docs/recordhound.md)** | Music. Works with ListenBrainz, Spotify, Lidarr and Last.fm. Port 8789. |

## Install

Search for **Filmhound** or **Recordhound** in Community Apps and click Install. The defaults work: data goes to `/mnt/user/appdata/<app>`, and the apps run as `nobody:users` (99:100) like other Unraid apps. Open the WebUI, and the first start takes you to Settings.

Updates appear in Unraid's Docker tab when a new version is released.

## Support

Open an issue in this repository: <https://github.com/ShadeRF/unraid-templates/issues>.

## What's in this repository

- `templates/`: the Community Apps templates
- `icons/`: app icons
- `docs/`: user guides
- `ca_profile.xml`: the profile shown in Community Apps

The templates, icons and docs here are MIT licensed. The apps themselves are distributed as container images at `ghcr.io/shaderf/filmhound` and `ghcr.io/shaderf/recordhound`.
