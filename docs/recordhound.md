<p align="center"><img src="../icons/recordhound.png" width="96" alt=""><br>
<picture><source media="(prefers-color-scheme: dark)" srcset="../icons/recordhound-wordmark.svg"><img src="../icons/recordhound-wordmark-light-bg.svg" height="60" alt="Recordhound"></picture></p>

Music recommendations built from your Plex library and listening history. Browse new artists, see why each one was picked, preview them, and send what you want to Lidarr. Nothing is downloaded automatically.

## What you need

- A Plex server with a music library, and its token
- A free Last.fm API key ([last.fm/api/account/create](https://www.last.fm/api/account/create); any app name, callback URL can be blank)
- Optional: a Last.fm or ListenBrainz account with your scrobbles, Spotify, and Lidarr

## Setup

1. Install from Community Apps and open the WebUI (`http://SERVER-IP:8789`).
2. Settings opens on first start. Enter your Plex URL and token, and your Last.fm key. Use **Test** on each, then **Save**.
3. The first sync looks up a few hundred artists on Last.fm and takes several minutes. Lookups are cached for a month, so later syncs are quick. Syncs run nightly.

## What's in it

- **For You**: top picks, *Because you play…*, genre rows, deep cuts, new releases from artists you love, and albums you're missing.
- **All Picks**: every pick, endlessly, with genre include/exclude and filters for how well known an artist is.
- **You Stream**: artists you play a lot on Last.fm, ListenBrainz or Spotify but don't own. Send them to Lidarr from here.
- **Artist pages**: 30-second previews, why it was picked, bio, albums (owned ones marked), similar artists, and links to Spotify, Apple Music, Bandcamp and more.
- **Lidarr**: add artists with your quality and metadata profiles and choose what to monitor.
- **Save**, **Not interested**, **Already know them**, and **Don't learn from** (for kids' music or someone else's albums).

## Listening history

Plex play counts (including Plexamp) and star ratings are always used. Optionally add:

- **Last.fm**: enter your username.
- **ListenBrainz**: enter your username (your profile must be public).
- **Spotify history file**: request your data at [spotify.com/account/privacy](https://www.spotify.com/account/privacy/) and upload the zip Spotify emails you. No developer account needed.
- **Spotify account**: keeps your top, followed and saved artists current. Spotify only allows this through a personal developer app: create one at [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) with the redirect URI `http://127.0.0.1:8789/callback`, paste its Client ID in Settings, click **Connect Spotify**, approve, then paste back the address of the page that fails to load. Spotify requires Premium for developer apps, limits each to 5 users, and ends connections after six months.

## How it picks

Your star ratings count most, then how much you play an artist anywhere, then what you own (adjustable). Recordhound walks Last.fm's similar-artist data out from your strongest artists, scores candidates against a profile of the genres and scenes you return to, and explains each pick with the artists that led to it.

## HTTPS

Either works:

- **Reverse proxy (recommended):** put the app behind Nginx Proxy Manager, SWAG, Caddy, Traefik, or `tailscale serve`, and let it handle certificates. Proxies on your own network are trusted automatically, so the app knows it's on HTTPS (sign-in cookies are then marked secure). Serve it at the root of a domain or subdomain, e.g. `https://recordhound.example.com`; a sub-path like `/recordhound` isn't supported.
- **Built-in:** put a certificate and key in the Data folder (e.g. `certs/cert.pem` and `certs/key.pem`), then set **HTTPS certificate** to `/data/certs/cert.pem` and **HTTPS key** to `/data/certs/key.pem` in the container's advanced settings. Restart after renewing a certificate. With Tailscale, `tailscale cert` creates both files for your server's `ts.net` name.

If you turn on HTTPS, also turn on sign-in in Settings before reaching the app from outside your home.

## Tips

- Raise *Minimum Last.fm listeners* in Settings for better-known picks, or lower it and use **Deep cuts** for obscure ones.
- Your data is in the Data folder (`recordhound.db`, `settings.json`). Delete both to start fresh.
