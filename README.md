<p align="center">
  <img src="./doc/icon.png" alt="Reel Mind" width="72" height="72" />
</p>

<h1 align="center">Reel Mind</h1>

<p align="center">
  把知识类短视频整理成可搜索、可复习、可追问的 AI 笔记。
</p>

Reel Mind 是一个面向抖音精选知识视频的本地知识管理工具。输入视频链接后，它可以完成视频解析、音频转写、AI 总结，并生成 Markdown 笔记、思维导图和知识卡片。

## 主要功能

- 解析抖音精选视频并生成结构化笔记
- 音频转写与 AI 总结
- Markdown、思维导图和知识卡片视图
- 收藏、标签、备注和历史记录
- 基于当前笔记或知识库进行 AI 问答
- 对关键内容进行联网核验
- 通过浏览器扩展同步抖音 Cookie

## 快速开始

目前推荐在 Windows 上使用本地启动脚本。开始前请安装：

- Git
- Python 3.11+
- Node.js 20+
- Corepack
- FFmpeg

### 1. 克隆项目

```powershell
git clone https://github.com/seintbe/reelmind.git
cd reelmind
```

### 2. 安装后端依赖

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
cd ..
```

### 3. 安装前端依赖

```powershell
cd reel-mind-frontend
corepack enable
pnpm install
cd ..
```

### 4. 启动项目

双击 `run.bat`，或在 PowerShell 中运行：

```powershell
.\run.bat
```

启动完成后访问：

```text
http://127.0.0.1:3015/
```

常用命令：

```powershell
.\run.bat --check    # 检查依赖
.\run.bat --status   # 查看服务状态
.\run.bat --stop     # 停止服务
.\run.bat --no-open  # 启动后不自动打开浏览器
```

## 使用方法

1. 打开 Web 页面，在设置中配置模型供应商、Base URL、模型和 API Key，并测试连接。
2. 输入抖音精选视频链接。
3. 根据需要填写收藏夹、标签和备注。
4. 点击“生成笔记”，等待解析、转写和总结完成。
5. 在 Markdown、思维导图、知识卡片或 AI 问答视图中查看结果。

如果视频需要登录状态，请按[扩展说明](./reel-mind-extension/README.md)完成构建，在浏览器中加载 `reel-mind-extension/extension/`，然后同步抖音 Cookie。

生成的笔记默认保存在：

```text
backend/note_results/
```

## 配置

首次运行 `run.bat` 时会自动创建根目录 `.env`。也可以复制 `.env.example` 后手动修改。

常用配置：

| 变量 | 说明 | 默认值 |
| --- | --- | --- |
| `BACKEND_PORT` | 后端端口 | `8483` |
| `VITE_FRONTEND_PORT` | 前端端口 | `3015` |
| `TRANSCRIBER_TYPE` | 转写方式 | `bcut` |
| `WHISPER_MODEL_SIZE` | Whisper 模型大小 | `tiny` |
| `NOTE_OUTPUT_DIR` | 笔记输出目录 | `note_results` |
| `FFMPEG_BIN_PATH` | FFmpeg 路径，留空时使用系统 PATH | 空 |

模型供应商和 API Key 建议直接在 Web 设置页面中配置。

使用 Brave 进行联网核验时，还需要在 `.env` 中填写 `BRAVE_SEARCH_API_KEY`。

## 可选：Docker

请先安装 Docker Desktop，并准备环境配置：

```powershell
Copy-Item .env.example .env
docker compose up -d --build
```

Docker 启动后同样访问 `http://127.0.0.1:3015/`。停止服务：

```powershell
docker compose down
```

## 项目结构

```text
backend/                FastAPI 后端
reel-mind-frontend/     React Web 前端
reel-mind-extension/    浏览器扩展
run.bat                 Windows 本地启动脚本
docker-compose.yml      Docker Compose 配置
```

## 相关文档

- [详细使用说明](./README-usage.md)
- [部署说明](./DEPLOYMENT.md)
- [产品使用指南](./task/ReelMind_使用指南.md)

## 许可证

本项目基于 [MIT License](./LICENSE) 开源。
