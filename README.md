# Terra Ocean-Only Overworld Config (based on default)

This is a Terra 6.0+ configuration pack that makes the Overworld biome distribution essentially **ocean-only**, so the world feels like an “all ocean” overworld.

## What it changes

The key selection happens in `pack.yml`, which enables the ocean preset:
- `pack.yml` -> `$biome-providers/presets/ocean.yml:biomes`
- `biome-providers/presets/ocean.yml` -> uses `biome-providers/sources/ocean_only.yml`
- `biome-providers/sources/ocean_only.yml` -> only includes `ocean` and `deep-ocean`

Everything else follows Terra’s normal pipeline/stages.

## Customization (optional)

- More/less `deep-ocean` vs `ocean`: edit `biome-providers/sources/ocean_only.yml` weights.
- Bigger/smaller ocean regions: tweak `meta.yml` under `biome-distribution`.

Terra project: https://github.com/PolyhedralDev/Terra
