# 泌尿系感染性结石随访管理循证智能助手 — 静态部署包

## 目录结构

```
infectious-stone-agent-v2/
├── index.html                          # 入口 HTML（SPA，所有路由均指向此文件）
├── assets/
│   ├── index-DYvoYWBg.css             # 全局样式（Tailwind CSS 4 + 自定义主题）
│   └── index-P9DfuEw9.js             # 应用主包（React 19 + 所有页面逻辑）
├── manus-storage/
│   ├── hospital-logo_e2aa6806.webp   # 广医一院泌尿外科 Logo（圆形徽章）
│   └── qrcode_blue_3b02e5a1.png      # 蓝色带Logo二维码（指向发布网址）
└── README.md                          # 本说明文件
```

---

## Logo 使用说明

### Header（顶部导航栏）
- **文件**：`manus-storage/hospital-logo_e2aa6806.webp`
- **容器尺寸**：40×40 px（`w-10 h-10`，圆形裁切 `rounded-full`）
- **位置**：页面顶部固定导航栏左侧，紧邻"广州医科大学附属第一医院 / 泌尿外科"文字

### 首页 Hero 区域
- **文件**：`manus-storage/hospital-logo_e2aa6806.webp`
- **容器尺寸**：120×120 px 圆形白色背景卡片，内部图片 108×108 px（`object-contain`）
- **位置**：首页居中 Hero 区域，标题文字上方，页面纵向约 10% 处
- **样式**：白色圆形背景 + 蓝色细边框光晕（`ring-1 ring-[#DCE8F7]`）+ 阴影

### 二维码中心 Logo
- **文件**：`manus-storage/qrcode_blue_3b02e5a1.png`（已内嵌于二维码图片中）
- **二维码展示尺寸**：160×160 px（`h-[160px] w-[160px]`）
- **位置**：首页底部"扫码访问智能助手"区域

---

## 部署方式

### Nginx / Apache 静态托管
1. 将所有文件上传至 Web 服务器根目录
2. **关键配置**：所有路由（`/assessment`、`/knowledge`、`/registration`）均需重定向到 `index.html`（SPA 路由）

**Nginx 配置示例：**
```nginx
server {
    listen 80;
    root /var/www/infectious-stone;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /manus-storage/ {
        alias /var/www/infectious-stone/manus-storage/;
    }
}
```

### 注意事项
- `manus-storage/` 目录中的图片文件需与 `index.html` 保持**同级目录**关系
- 代码中图片引用路径为绝对路径：`/manus-storage/hospital-logo_e2aa6806.webp`
- 字体使用系统内置**微软雅黑**（Microsoft YaHei），无需加载外部字体文件

---

## 页面路由

| 路径 | 页面 | 功能说明 |
|------|------|---------|
| `/` | 首页 | Logo + 功能入口 + 二维码 |
| `/assessment` | 随访评估 | 症状自测、指标参考、风险分级、随访时间表 |
| `/knowledge` | 健康知识 | 8大循证类别（可折叠展开），含证据等级标注 |
| `/registration` | 随访登记 | 4个Tab表单（基本信息、手术指标、临床随访、护理随访） |

---

## 技术栈

- **框架**：React 19 + TypeScript
- **路由**：Wouter 3
- **样式**：Tailwind CSS 4 + shadcn/ui
- **动画**：Framer Motion 12
- **图标**：Lucide React
- **字体**：微软雅黑（系统字体，无外部依赖）
- **构建**：Vite 7

---

*证据来源：《泌尿系感染性结石患者随访管理的最佳证据总结》*
*本工具仅供医护人员参考，不替代临床诊断*
