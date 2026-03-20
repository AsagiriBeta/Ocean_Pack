# Terra 全海洋地形包（基于 default 魔改）

这是一个面向 Terra 6.0+ 的「地形配置包」，目标是让生成的 Overworld 世界在**生物群系分布层面**几乎只由海洋类群系组成，从而呈现“全为海洋”的世界观。

该包是在 Terra 官方 default Overworld 配置的基础上魔改而来；因此多数目录结构与默认版本一致，差异主要集中在「海洋/陆地分布（biome distribution）」相关配置上。

Terra 官方项目（供参考）：
<https://github.com/PolyhedralDev/Terra>

---

## 核心实现：为什么会“全海洋”

你可以按下面这条链路直接在配置文件里验证：

1. `pack.yml` 选择了海洋预设（biome distribution preset）
   - `./pack.yml`
   - 其中 `biomes:` 指向：`$biome-providers/presets/ocean.yml:biomes`

2. `biome-providers/presets/ocean.yml` 指定了“海洋专用 source”
   - `./biome-providers/presets/ocean.yml`
   - 它的 pipeline 里启用了：`source: $biome-providers/sources/ocean_only.yml:source`

3. `biome-providers/sources/ocean_only.yml` 只允许 ocean / deep-ocean
   - `./biome-providers/sources/ocean_only.yml`
   - 该文件的 `biomes` 只包含：
     - `ocean`
     - `deep-ocean`

由于整个世界的“群系归属”只落在这些海洋类群系上，因此视觉上会更接近全海洋；同时其它 stages/features 仍沿用默认流程，因此你可能仍会看到海底植被、海洋地形变体、河流等（但不会出现陆地群系主导的大片陆地）。

---

## 使用方式（简要）

将本目录作为一个 Terra 配置包导入（具体放置位置/加载方式请以你使用的 Terra 版本与启动方式为准；这里的关键是 `pack.yml` 会被识别）。

导入后，只要 Terra 读取到本包里的 `pack.yml`，就会应用上面这些“全海洋”配置链路。

---

## 自定义/调整

### 生成更偏“浅海 ocean”还是“深海 deep-ocean”

修改 `./biome-providers/sources/ocean_only.yml` 中对应的权重（例如当前是 `ocean: 2`、`deep-ocean: 1`）。

### 调整群系分布尺度（海洋/深海区域更大或更碎）

修改 `./meta.yml` 里的 `biome-distribution` 参数（例如 `continental-scale`、`elevation-scale` 等）。

### 恢复到默认（出现陆地/混合群系）

把 `./pack.yml` 里的 `biomes:` 从 `ocean.yml` 改回默认预设，例如：

- `$biome-providers/presets/default.yml:biomes`

或按需使用 `./biome-providers/presets/single.yml` 指定单一群系。
