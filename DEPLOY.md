# 部署方案

> 注意：页面包含真实账户资产与持仓数据，**不要部署到无访问控制的公开地址**。

## 方案 A：本地双击（零部署，推荐日常使用）

直接双击 `ats-s100.html`。实时行情接口（东方财富）允许跨域，file:// 打开也能刷新行情。

## 方案 B：局域网手机查看（免费、数据不出门）

在仓库目录跑一个静态服务器，手机连同一 Wi-Fi 访问电脑 IP：

```bash
cd /Volumes/Samsung_T5/kimicode
python3 -m http.server 8000
# 手机浏览器打开 http://<电脑IP>:8000/ats-s100.html
```

页面已做移动端响应式（<768px 为顶部栏+底部标签导航）。

## 方案 C：Cloudflare Pages（有外网访问需求时）

1. cloudflare.com 注册（免费），Workers & Pages → Create → Pages → Upload assets
2. 上传 `ats-s100.html` 为 index.html，得到一个 `*.pages.dev` 地址
3. **必须加访问控制**：Pages 不能单独加密码，用 Cloudflare Access（免费版支持 50 用户）给该域名加登录，或改用 Netlify（免费版支持站点密码）

## 方案 D：GitHub Pages（不推荐）

免费版 Pages 仅支持公开仓库，页面里的账户数据会公开；私有 Pages 需要付费 Pro。如坚持：
Settings → Pages → Source 选 main 分支根目录。

## 移动端适配说明

- viewport 自适应；≥1024px 左侧边栏，768–1023px 图标窄栏，<768px 顶部横条 + 底部标签导航
- 卡片单列堆叠、K 线图 viewBox 自适应、所有表格横向滑动
- 竖屏查看 K 线/驾驶舱为最佳；复杂表格建议横屏

## 实时行情接口

- 行情：东方财富 `push2.eastmoney.com/api/qt/ulist.np/get`（30 秒轮询，可开关）
- K 线：`push2his.eastmoney.com/api/qt/stock/kline/get`
- 均为免费公开接口、无 key；接口失效时自动回退静态数据并显示"离线"徽标
