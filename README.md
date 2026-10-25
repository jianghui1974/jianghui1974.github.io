# Jianghui — 总主页

GitHub Pages 的用户站点，对应 <https://jianghui1974.github.io/>。
这个仓库只放总主页；两个产品各自的站点在各自的仓库里：

| 站点 | 仓库 | 地址 |
|---|---|---|
| Quileg HID | `jianghui1974/Quileg-HID` | <https://jianghui1974.github.io/Quileg-HID/> |
| 孤云 Guyun | `jianghui1974/Guyun` | <https://jianghui1974.github.io/Guyun/> |

仓库名必须是 `jianghui1974.github.io`，Pages 才会把它挂在根域名上。

## 文件

```
index.html        主页（单页，无构建步骤）
styles.css        全部样式，含深色模式
assets/mark.svg   站点标记（蓝 + 青两个方块）与 favicon
assets/og.png     分享卡片图 1200×630
assets/*-icon.png 两个产品的图标（从各自站点取，256px / 180px）
og.html           og.png 的源文件，用浏览器截图得到，不对外链接
preview-*.png     本地预览截图，已 gitignore
```

## 改内容

- 文案、链接：直接改 `index.html`
- 颜色、间距：`styles.css` 顶部的 `:root` 变量；两个产品色是 `--quileg` 与 `--guyun`
- 产品图标换了：从对应站点下载新图标，覆盖 `assets/` 下的同名文件
- 分享图改了：改 `og.html`，然后重新截图

```bash
CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
"$CHROME" --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --window-size=1200,630 --force-device-scale-factor=1 \
  --screenshot="assets/og.png" "file://$PWD/og.html"
```

（`--no-sandbox` 是因为这是在沙箱里跑 Chrome；在普通终端里可以去掉。）

## 本地预览

直接开 `index.html` 就行，没有构建、没有依赖、没有外部请求。
深色模式跟随系统；想临时强看一下，把 `styles.css` 里
`@media (prefers-color-scheme: dark)` 改成 `@media all`。

## 发布

```bash
git add -A && git commit -m "home: …" && git push origin main
```

Pages 会在 30–60 秒内重建。首次发布需要仓库存在且 Pages 已开启
（Source: `main` 分支，目录 `/`）。

## 注意

- 页面上写的都是两个产品官网上已经写明的事；改文案时别加没验证过的承诺
  （比如「不做遥测」目前只有孤云官网明确写了）。
- 两个产品的版本号、下载按钮的落地页都不在这里写死，链接指向各自的站点或
  `releases/latest`，避免过期。
