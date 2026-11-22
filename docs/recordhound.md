<p align="center"><img src="../icons/recordhound.png" width="96" alt=""><br>
<picture><source media="(prefers-color-scheme: dark)" srcset="../icons/recordhound-wordmark.svg"><img src="../icons/recordhound-wordmark-light-bg.svg" height="60" alt="Recordhound"></picture></p>

Music recommendations built from your Plex library and listening history. Browse new artists, see why each one was picked, preview them, and send what you want to Lidarr. Nothing is downloaded automatically.

I built Recordhound because the recommendation apps I tried never matched what was in my library or what I listen to. It starts from your own library, explains every pick, and lets you tune how it decides.

<p align="center"><img src="../screenshots/recordhound-for-you.jpg" alt="For You: top picks, each with the artists that led to it"></p>

## What you need

- A Plex server with a music library, and its token
- Optional: a ListenBrainz account with your scrobbles, Spotify, Lidarr, and a Last.fm API key (see [Last.fm](#lastfm))

## Setup

When installing, Community Apps asks which version you want: **Latest** (stable releases, recommended) or **Nightly** (built every night from the newest code, with new features first and the occasional bug). You can switch any time by editing the container and changing the tag at the end of Repository, for example `ghcr.io/shaderf/recordhound:latest`. Your settings and data carry over. Two more tags exist for special cases: an exact version such as `:0.13.0` to stay on one release or roll back if a release causes trouble, and `:edge`, test builds published while changes are being tried out (expect rough edges).


1. Install from Community Apps and open the WebUI (`http://SERVER-IP:8789`).
2. A short setup walkthrough opens on first start. Enter your Plex URL and token and use **Test**. Everything else is optional: the **Getting started** list on the home page points to the extras, and everything can be changed later in Settings.
3. The first sync looks up every artist and can take 20 minutes or more, since MusicBrainz allows one lookup a second. Lookups are cached for a month, so later syncs are quick. Syncs run nightly.

## What's in it

- **For You**: a *This week* summary, top picks (reshuffled weekly), *New for you this week*, *Because you play…*, genre rows, deep cuts, new releases from artists you love (including announced albums), albums you're missing, and albums you own but never played.
- **All Picks**: every pick, endlessly, with genre include/exclude and filters for how well known an artist is.
- **Your Library**: albums you own but have never played, ranked for you with a reason for each. One click puts the top ones in a Plex playlist for Plexamp.
- **You Stream**: artists you play a lot on Last.fm, ListenBrainz or Spotify but don't own. Send them to Lidarr from here.
- **Rate**: rate the artists you play, one at a time. Ratings go to Plex. Rate picks you already know so they stop being suggested.
- **Artist pages**: 30-second previews, why it was picked, bio, albums (owned ones marked), similar artists, and links to Spotify, Apple Music, Bandcamp and more.
- **Lidarr**: add artists with your quality and metadata profiles and choose what to monitor.
- **Save**, **Not interested**, **Already know them**, and **Don't learn from** (for kids' music or someone else's albums).

## Listening history

Plex play counts (including Plexamp) and star ratings are always used. Optionally add:

- **Last.fm**: enter your username. This needs a Last.fm API key, and from December 1, 2026 the key's account needs Last.fm Pro.
- **ListenBrainz**: enter your username (your profile must be public).
- **Spotify history file**: request your data at [spotify.com/account/privacy](https://www.spotify.com/account/privacy/) and upload the zip Spotify emails you. No developer account needed.
- **Spotify account**: keeps your top, followed and saved artists current. Spotify only allows this through a personal developer app: create one at [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) with the redirect URI `https://shaderf.github.io/recordhound-auth/`, paste its Client ID in Settings, click **Connect Spotify** and approve. You come straight back. (That address is a small page that sends you back to your own Recordhound; [how it works](https://github.com/ShadeRF/recordhound-auth).) If you connected Spotify before this was possible, see the note in Settings → Spotify. Spotify requires Premium for developer apps, limits each to 5 users, and ends connections after six months.

## How it picks

Your star ratings count most, then how much you play an artist anywhere, then what you own (adjustable). Artists you've played in the last six months get extra pull (adjustable under *What you've played lately*). Recordhound walks similar-artist data out from your strongest artists, scores candidates against a profile of the genres and scenes you return to, and explains each pick with the artists that led to it.

### Where artist data comes from

By default, similar artists come from ListenBrainz (what its listeners play together) and Deezer (related artists), genre tags from MusicBrainz, fan counts from Deezer, and bios from Wikipedia. None of these need a key.

<a id="lastfm"></a>**Last.fm:** if you enter a Last.fm API key, Recordhound uses Last.fm's similar artists, tags and listener counts instead, and can read your scrobbles. From December 1, 2026, Last.fm keys only work while the account that owns the key has Last.fm Pro. If your key stops working, Recordhound switches to the free sources on its own and shows a warning; clear the key in Settings to make that permanent.

## HTTPS

Either works:

- **Reverse proxy (recommended):** put the app behind Nginx Proxy Manager, SWAG, Caddy, Traefik, or `tailscale serve`, and let it handle certificates. Proxies on your own network are trusted automatically, so the app knows it's on HTTPS (sign-in cookies are then marked secure). Serve it at the root of a domain or subdomain, e.g. `https://recordhound.example.com`; a sub-path like `/recordhound` isn't supported.
- **Built-in:** put a certificate and key in the Data folder (e.g. `certs/cert.pem` and `certs/key.pem`), then set **HTTPS certificate** to `/data/certs/cert.pem` and **HTTPS key** to `/data/certs/key.pem` in the container's advanced settings. Restart after renewing a certificate. With Tailscale, `tailscale cert` creates both files for your server's `ts.net` name.

If you turn on HTTPS, also turn on sign-in in Settings before reaching the app from outside your home.

## Tips

- Rating artists is the biggest lever. The **Rate** page makes it quick.
- Raise *Minimum Deezer fans* (or *Minimum Last.fm listeners* with a Last.fm key) in Settings for better-known picks, or lower it and use **Deep cuts** for obscure ones.
- Your data is in the Data folder (`recordhound.db`, `settings.json`). Delete both to start fresh.

*Filmhound and Recordhound are named for Daisy, my beagle and the hound of my life.*

## Source code and help

Recordhound is open source under the AGPL-3.0: [github.com/ShadeRF/recordhound](https://github.com/ShadeRF/recordhound). Report problems or suggest ideas in its [issues](https://github.com/ShadeRF/recordhound/issues).
