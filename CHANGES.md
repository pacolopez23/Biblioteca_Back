# Changes from upstream Jellyfin

This repository is a fork of [jellyfin/jellyfin](https://github.com/jellyfin/jellyfin).
It is not affiliated with, endorsed by, or supported by the Jellyfin project.

Licensed under GPL-2.0-or-later, same as upstream. The original `LICENSE` and all
copyright notices are preserved. This file records the modifications made to the
original work, as required by section 2(a) of the GPL.

Base: branch `release-12.z`, commit `3c698bab7f` (11 September 2026).

## 2026-09-12 — Security

**URL-encode provider ids in external URLs** (`MediaBrowser.Providers/`, 13 files)

External URL providers interpolated the raw provider id into the URL string.
Provider ids are only format-validated for Imdb, Tmdb, AudioDb and MusicBrainz;
for any other provider the value is stored unchecked, and it can be set from an
NFO file in the media folder. Every provider id is now wrapped in
`Uri.EscapeDataString`.
