# Filmhound & Recordhound for Unraid

Self-hosted recommendation apps for Plex. Both build picks from **your own library and history**, show **why** each one was picked, and never download anything on their own.

| | | |
|---|---|---|
| <img src="icons/filmhound.png" width="72"> | **[Filmhound](docs/filmhound.md)** | Movies and TV. Works with Seerr, Radarr, Sonarr, Letterboxd and Trakt. Port 8788. |
| <img src="icons/recordhound.png" width="72"> | **[Recordhound](docs/recordhound.md)** | Music. Works with ListenBrainz, Spotify, Lidarr and Last.fm. Port 8789. |

Both are open source under the AGPL-3.0: [Filmhound source](https://github.com/ShadeRF/filmhound) · [Recordhound source](https://github.com/ShadeRF/recordhound).

## Install

Search for **Filmhound** or **Recordhound** in Community Apps and click Install. The defaults work: data goes to `/mnt/user/appdata/<app>`, and the apps run as `nobody:users` (99:100) like other Unraid apps. Open the WebUI, and a short walkthrough on the first start gets you connected.

Updates appear in Unraid's Docker tab when a new version is released.

## Support

For problems with an app, open an issue in its own repository: [Filmhound](https://github.com/ShadeRF/filmhound/issues) or [Recordhound](https://github.com/ShadeRF/recordhound/issues). Problems with the Unraid templates themselves can go [here](https://github.com/ShadeRF/unraid-templates/issues).

## What's in this repository

- `templates/`: the Community Apps templates
- `icons/`: app icons
- `docs/`: user guides
- `ca_profile.xml`: the profile shown in Community Apps

The templates and docs here are MIT licensed. The icons and wordmarks in `icons/` are not: the Filmhound and Recordhound names and logos may only be used to refer to the official apps (see [icons/README.md](icons/README.md)). The apps are distributed as container images at `ghcr.io/shaderf/filmhound` and `ghcr.io/shaderf/recordhound`.
