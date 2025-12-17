# Sources 资源目录

本目录包含从目标网站爬取的所有 Sources 面板资源文件。

## 目录说明

本目录存储了通过 Puppeteer 爬虫从网页的 Sources 面板（浏览器开发者工具中的 Sources 标签页）中提取并下载的所有资源文件。

## 目录结构

```
sources/
├── README.md                          # 本说明文件
├── sources_list.json                 # 资源列表清单（包含所有下载资源的元数据）
│
├── assets/                            # 静态资源文件
│   ├── font/                         # 字体文件
│   ├── image/                        # 图片文件
│   └── svg/                          # SVG 矢量图
│
├── static/                            # 静态文件（CSS、JS等）
│   ├── css/                          # 样式表文件
│   ├── js/                           # JavaScript 文件
│   └── preset-browser@12.0.1/        # 浏览器预设文件
│
├── external/                          # 外部域名资源
│   ├── account.djicdn.com/          # DJI 账户中心 CDN 资源
│   ├── allears.djicdn.com/           # DJI 相关资源
│   ├── static.djicdn.com/             # DJI 静态资源 CDN
│   ├── res.wx.qq.com/                # 微信相关资源
│   └── [其他外部域名]/                # 其他跨域资源
│
├── Cesium-1.116.0-fix-26/            # Cesium 3D 地图库
│   ├── Cesium.js                     # 主库文件
│   ├── Widgets/                      # 组件样式
│   └── Assets/                       # 资源文件（地形数据等）
│
├── wasm-v06.17.00.02/                 # WebAssembly 模块
│   ├── libppe.js / libppe.wasm       # PPE 相关模块
│   ├── libwpmz.js / libwpmz.wasm     # WPMZ 相关模块
│   └── *.worker.js                    # Web Worker 文件
│
├── lidar-wasm-v11/                    # 激光雷达 WASM 模块
│   ├── liblidar.js / liblidar.wasm
│   └── wayline.lidar.worker.js
│
├── ar-wasm-2025.11-6/                 # AR 增强现实 WASM 模块
│   ├── ArCore.js
│   └── ArCore.wasm
│
├── mine-decoder/                       # 解码器模块
│   ├── MineDecoder.js
│   └── MineDecoder.wasm
│
├── map-app/                           # 地图应用
│   ├── index.html
│   └── static/
│
├── message-app/                       # 消息应用
│   ├── index.html
│   └── static/
│
├── project-list-app/                  # 项目列表应用
│   ├── index.html
│   └── static/
│
├── user-center-app/                   # 用户中心应用
│   ├── index.html
│   └── static/
│
├── benchmarks-1.0/                    # 性能基准测试数据
│   └── d-intel.json
│
├── paas-core.*.js                     # 平台即服务核心文件
├── paas.css                           # 平台样式表
└── fh-favicon.ico                     # 网站图标
```

## 资源类型

### 1. JavaScript 文件
- **主应用文件**：`paas-core.*.js`、各应用的 `index.*.js`
- **库文件**：Vue、Axios、Router、Polyfill 等
- **组件包**：`component-package.*.js`、`common-package.*.js`
- **外部库**：来自 `account.djicdn.com` 等 CDN 的 JS 文件

### 2. CSS 样式表
- **主样式**：`paas.css`、`index.*.css`
- **组件样式**：`component-package.*.css`、`common-package.*.css`
- **第三方样式**：Cesium Widgets 样式等

### 3. WebAssembly (WASM) 文件
- **PPE 模块**：`libppe.js` / `libppe.wasm` - 可能用于图像处理
- **WPMZ 模块**：`libwpmz.js` / `libwpmz.wasm` - 可能用于数据压缩
- **激光雷达模块**：`liblidar.js` / `liblidar.wasm` - 用于激光雷达数据处理
- **AR 模块**：`ArCore.js` / `ArCore.wasm` - 用于增强现实功能
- **解码器**：`MineDecoder.js` / `MineDecoder.wasm` - 用于数据解码

### 4. 静态资源
- **图片**：JPG、PNG、SVG、WebP 格式
- **字体**：TTF、WOFF、WOFF2 格式
- **图标**：ICO 格式

### 5. 应用模块
- **地图应用** (`map-app`)：基于 Cesium 的 3D 地图功能
- **消息应用** (`message-app`)：消息通知功能
- **项目列表应用** (`project-list-app`)：项目管理功能
- **用户中心应用** (`user-center-app`)：用户管理功能

### 6. 第三方库
- **Cesium**：3D 地球和地图可视化库
- **Vue.js**：前端框架
- **Axios**：HTTP 客户端
- **Vue Router**：路由管理

## sources_list.json

`sources_list.json` 文件记录了所有下载资源的详细信息，包括：

```json
{
  "timestamp": "2025-12-17T15:41:19.988Z",  // 下载时间戳
  "total": 74,                              // 总资源数
  "downloaded": 94,                         // 成功下载数
  "failed": 109,                            // 失败数
  "sourcesDir": "./downloads/sources",      // 资源目录路径
  "resources": [                            // 资源列表
    {
      "url": "资源URL",
      "path": "本地保存路径",
      "size": 文件大小（字节）,
      "contentType": "MIME类型",
      "status": "downloaded|exists|failed",  // 状态
      "error": "错误信息（如果失败）"
    }
  ]
}
```

## 使用说明

### 查看资源列表

```bash
# 查看资源列表文件
cat sources_list.json | jq

# 或者使用 Node.js
node -e "console.log(JSON.stringify(require('./sources_list.json'), null, 2))"
```

### 统计信息

```bash
# 统计成功下载的资源数量
cat sources_list.json | jq '.resources | map(select(.status == "downloaded" or .status == "exists")) | length'

# 统计失败的资源数量
cat sources_list.json | jq '.resources | map(select(.status == "failed")) | length'

# 按文件类型统计
cat sources_list.json | jq '.resources | group_by(.contentType) | map({type: .[0].contentType, count: length})'
```

### 查找特定资源

```bash
# 查找包含特定关键词的资源
cat sources_list.json | jq '.resources[] | select(.url | contains("cesium"))'

# 查找特定域名的资源
cat sources_list.json | jq '.resources[] | select(.url | contains("fh.dji.com"))'
```

## 注意事项

1. **文件完整性**：某些资源可能因为网络问题、权限限制或服务器错误而下载失败，这些信息会记录在 `sources_list.json` 中。

2. **跨域资源**：来自不同域名的资源会保存在 `external/` 目录下，按域名组织。

3. **文件大小**：WASM 文件和大型 JavaScript 库文件可能较大，请确保有足够的磁盘空间。

4. **版本信息**：文件名中包含版本号或哈希值（如 `paas-core.42b16654be65982806e5.js`），这些用于缓存控制。

5. **依赖关系**：某些资源文件之间存在依赖关系，单独使用可能无法正常工作。

## 技术栈

从下载的资源可以看出，目标网站使用了以下技术栈：

- **前端框架**：Vue.js
- **3D 可视化**：Cesium
- **高性能计算**：WebAssembly (WASM)
- **HTTP 客户端**：Axios
- **路由管理**：Vue Router
- **构建工具**：Webpack（从文件名格式推断）

## 更新说明

本目录由爬虫脚本自动生成和维护。每次运行爬虫时，新的资源会被下载并更新到 `sources_list.json` 中。

---

**生成时间**：2025-12-17  
**爬虫版本**：1.0.0  
**目标网站**：https://fh.dji.com/

