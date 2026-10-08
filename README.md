# JobPilot - 网申搭档

Chrome / Microsoft Edge 浏览器侧边栏求职资料与逐项填写助手。

## 下载与安装

### Edge 商店安装（推荐）

[在 Microsoft Edge 商店安装 JobPilot](https://microsoftedge.microsoft.com/addons/detail/apcpkfhlajlfbkmekglbbkgacjjhglie)

已正式上架。使用 Edge 打开上方链接，在商店按提示安装即可，无需终端或开发者模式。

### Chrome / Edge 手动安装

下载本仓库中的 **JobPilot-Edge-store-v1.0.19.zip** 并解压。安装包已经构建完成，不需要 Node.js、npm 或终端。

1. Edge 打开 `edge://extensions`，Chrome 打开 `chrome://extensions`。
2. 开启开发者模式，点击“加载解压缩的扩展”。
3. 选择解压后包含 `manifest.json` 的文件夹。
4. 固定插件图标，在招聘页面点击图标打开侧边栏。

Edge 商店版本已正式上架；本仓库仍提供手动安装包。

## 使用

在“简历导入”手动选择中文或英文，上传 TXT、DOCX 或可提取文本的 PDF，解析后导入资料库。可以搜索、复制、编辑、删除资料，也可以建立自定义分组和记录。

在“当前页面”授权招聘网站并启用点击匹配。点击网页目标输入框，在侧边栏选择资料后逐项填写。多条经历请指定对应记录。日期及下拉选项在控件能可靠识别时辅助选择，网站兼容性存在差异。

插件不会提交申请，不自动添加经历，也不整页批量填写。使用前请备份资料，填写后检查网站显示结果。

本地解析和规则匹配不需要 AI 密钥。翻译是可选功能，需要浏览器支持或自行配置 AI 服务；服务提供商可能收费。

## 隐私与支持

资料默认保存在浏览器本地。选择云端 AI 功能后，相关文本会发送到用户指定的 HTTPS 服务。

[隐私政策](https://nikiwonjay.github.io/jobpilot-privacy/privacy.html)

支持邮箱：203171592@qq.com

本仓库提供可安装的构建包和说明。包内包含第三方依赖许可说明。

## 技术栈与架构

| 层级 | 技术 | 用途 |
| --- | --- | --- |
| 扩展平台 | Chromium Manifest V3 | Chrome / Edge 扩展，Service Worker 后台与侧边栏 |
| 界面 | React 19、TypeScript 5.9、CSS | 资料库、简历导入、设置与当前字段候选界面 |
| 构建 | Vite 7、TypeScript | 构建侧边栏、后台与独立内容脚本 |
| PDF 解析 | PDF.js（pdfjs-dist 6.3.289） | 本地提取文本型 PDF 内容；不包含 OCR |
| Word 解析 | Mammoth 1.10 | 本地提取 DOCX 文本 |
| 数据校验 | Zod 4 | 资料及导入数据结构校验 |
| 本地存储 | chrome.storage.local | 保存资料、映射、设置及用户配置的服务密钥 |
| 页面交互 | Content Script、DOM API、MutationObserver | 识别当前字段与动态控件，辅助单字段填写 |
| 扩展通信与授权 | chrome.runtime、tabs、scripting、activeTab、可选网站权限 | 连接侧边栏与目标页面，按用户操作访问网站 |
| 可选翻译 | 浏览器 Translator API | 浏览器支持时进行本地翻译 |
| 可选云端 AI | Fetch、用户配置的 HTTPS API | 使用用户指定的模型、服务地址与 API Key |
| 测试 | Vitest 4、jsdom 26 | 规则、数据处理和 DOM 控件行为测试 |

采用浏览器本地优先架构：侧边栏负责资料管理，后台负责扩展通信和授权，内容脚本负责识别网页字段并执行用户选定的填写操作。日期控件包含 Phoenix 日历适配及通用识别逻辑，无法可靠识别的控件保留手动处理方式。

开发环境使用 Node.js >=22.18.0 与 npm；用户安装本仓库的已构建 ZIP 不需要这些工具。当前仓库提供构建包，尚未上传完整开发源码。


