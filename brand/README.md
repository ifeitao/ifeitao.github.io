# brand/ — 站点图标源文件

图标沿用 secevo.xyz 的品牌标记「此身 · 年轮 · 火种」：三圈等距外扩，三个缺口同指 315°，
火种红圆点留在圈内。几何与配色照抄 SecEvo Labs 品牌素材包（200 单位画布，线宽 9 / 12.15）。

| 文件 | 用途 |
|---|---|
| `icon-tile.svg` | 进化绿圆角方 + 三圈，生成 `favicon.svg`、`favicon-32x32.png`、`favicon-96x96.png` |
| `icon-tile-mini.svg` | 同一枚方标，只留一环，用于 ≤16px 档（三圈在这个尺寸会糊成一团灰） |
| `icon-disc.svg` | 满版绿圆章 + 纸白细描边，生成 `logo.png`（页眉 64px 圆形）与安装图标 |

标准色：进化绿 `#1F4D3A`、火种红 `#D9472B`、宣纸白 `#F5F2EA`。
火种红只做圆点，不做文字。

改完源文件后重新生成 `static/` 下的全部位图：

```sh
python3 tools/make-icons.py
```

需要本机装有 Google Chrome（无头渲染）和 Pillow（拼装 `.ico`）。
