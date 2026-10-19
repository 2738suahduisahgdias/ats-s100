# 部署方案

> 仓库已公开，账户数据随页面公开（用户已确认接受）。外网部署：GitHub Pages 已开通。

## 方案 A：本地双击（零部署，推荐日常使用）

直接双击 `ats-s100.html`。实时行情接口（东方财富）允许跨域，file:// 打开也能刷新行情。

## 方案 B：局域网手机查看（免费、数据不出门）✅ 运行中

仓库目录运行静态服务器，手机连同一 Wi-Fi 访问电脑 IP：

```bash
cd /Volumes/Samsung_T5/kimicode
python3 -m http.server 8000 --bind 0.0.0.0
# 手机浏览器打开 http://192.168.0.3:8000/ats-s100.html
```

页面已做移动端响应式（<768px 为顶部栏+底部标签导航）。注意：电脑睡眠/关机或退出会话后服务会停止。

## 方案 C：GitHub Pages（外网访问）✅ 已部署

- 地址：https://2738suahduisahgdias.github.io/ats-s100/ats-s100.html
- 每次 `git push` 后约 1 分钟自动更新，无需额外操作
- 国内访问 github.io 偶尔较慢或不稳定，属网络层面问题，页面本身无依赖

## 方案 D：Cloudflare Pages / Netlify / Vercel（备选）

数据既然可公开，这三家免费静态托管都可直接用；优势是访问速度（尤其海外）与自动部署（绑定 GitHub 仓库 push 即发布）。Cloudflare Pages 国内速度通常好于 github.io。步骤：注册 → Pages → Connect to Git → 选 ats-s100 仓库 → 部署，几分钟完成。无需访问控制。

## 移动端适配说明

- viewport 自适应；≥1024px 左侧边栏，768–1023px 图标窄栏，<768px 顶部横条 + 底部标签导航
- 卡片单列堆叠、K 线图 viewBox 自适应、所有表格横向滑动
- 竖屏查看 K 线/驾驶舱为最佳；复杂表格建议横屏

## 实时行情接口

- 行情：东方财富 `push2.eastmoney.com/api/qt/ulist.np/get`（30 秒轮询，可开关）
- K 线：`push2his.eastmoney.com/api/qt/stock/kline/get`
- 均为免费公开接口、无 key；接口失效时自动回退静态数据并显示"离线"徽标
