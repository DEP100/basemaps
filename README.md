# basemaps

Self-hosted basemap tile/font/sprite assets for internal apps that need
offline or CSP-restricted map rendering (MapLibre GL + PMTiles), rather
than depending on a hosted tile provider at runtime.

Large binary assets in this repo are tracked with [Git LFS](https://git-lfs.com/)
— run `git lfs install` once per machine before cloning/pulling, or the
`.pmtiles` files will check out as small text pointer files instead of
real data.

## Layout

Each top-level directory is one basemap "flavor," self-contained:

```
conus/
  conus.pmtiles   # vector tiles, CONUS bbox only (-125,24,-66.5,49.5), 5 source-layers
  fonts/           # glyph PBFs, {fontstack}/{range}.pbf
  sprites/         # sprite JSON+PNG (@1x and @2x), dark flavor only
```

Produced by a `basemap/` pipeline (`extract.sh`/`trim.sh`/`fetch-assets.sh`)
that trims a public Protomaps/OSM build down to a specific bbox and a
handful of source-layers — see that pipeline for how to regenerate or
extend these assets (different bbox, additional source-layers, a light
flavor, etc.).

Meant to be reusable across projects that need this same self-hosted
basemap approach, via a git submodule for local dev or a tagged GitHub
Release for runtime download.
