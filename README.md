# 故事造梦间 · AI 网文 / 小说 / 短剧剧本生成器

> ✦ 把灵感写成大纲、章节与短剧

一个基于 **Streamlit + LangChain + DeepSeek（OpenAI 兼容接口）** 的 AI 创作 Web 应用。在左侧填好题材、主角、世界观和爽点，即可一键生成故事大纲、网文章节正文或可拍摄的短剧剧本；初稿可在页面上直接编辑、续写、修改，并导出 Markdown 保存。

- **在线体验**：Streamlit Cloud 部署链接见仓库 About 栏
- **主应用目录**：[`novel_script_ai/`](./novel_script_ai)（当前版本「故事造梦间」）
- **详细文档**：[`novel_script_ai/README.md`](./novel_script_ai/README.md)

---

## ✨ 功能特性

- **三种创作任务**
  - 📋 **故事大纲**：一句话核心、人物关系、故事规则、分卷 / 分集大纲、核心冲突与结尾走向
  - 📖 **网文章节**：可直接阅读的章节正文，开头尽快进入冲突，结尾留下阅读钩子
  - 🎬 **短剧剧本**：按场次编号，写明场景、时间、人物、动作与对白，每场推动冲突并设置反转 / 悬念
- **完整创作流程**：补全设定 → 生成初稿 → 在编辑器中直接修改 → 续写 / 改稿
- **续写与改稿**：支持「续写（接在原文后）」和「修改（替换原文）」两种后续操作，保持人物、设定与文风一致
- **可调参数**：篇幅（短 / 中 / 长）、创意程度（temperature 0.1–1.2）
- **结果导出**：一键下载 Markdown 文件，草稿仅保留在当前会话中
- **密钥安全**：API Key 只从本地 `.env` 或部署环境的 Secrets 读取，页面不接收、不展示密钥；报错信息中的密钥自动脱敏

## 🧱 技术栈

- **界面**：[Streamlit](https://streamlit.io/)
- **大模型接入**：[LangChain](https://python.langchain.com/) · `langchain-openai`（`ChatOpenAI`，OpenAI 兼容接口）
- **默认模型**：DeepSeek `deepseek-chat`（可通过环境变量切换其他兼容服务）
- **Python**：3.11.9

## 📁 目录结构

```
ai-novel-screenwriter/
├── novel_script_ai/              # 当前主应用（故事造梦间）
│   ├── app.py                    # Streamlit 主程序：设定面板、生成、续写 / 改稿、导出
│   ├── requirements.txt          # Python 依赖
│   ├── runtime.txt               # Streamlit Cloud 指定的 Python 版本
│   ├── .env.example              # 环境变量示例（复制为 .env 后填写）
│   ├── .gitignore
│   └── README.md                 # 详细使用文档
├── streamlit_app.py              # 早期版本：网文 + 短剧双模式生成器（历史保留）
└── .devcontainer/                # Dev Container 配置
```

## 🚀 快速开始

```bash
# 1. 克隆仓库
git clone https://github.com/fsy357/ai-novel-screenwriter.git
cd ai-novel-screenwriter/novel_script_ai

# 2. 安装依赖（建议先建虚拟环境）
pip install -r requirements.txt

# 3. 配置环境变量
cp .env.example .env   # Windows: Copy-Item .env.example .env
# 在 .env 中填入 DEEPSEEK_API_KEY

# 4. 启动
streamlit run app.py
```

浏览器打开终端提示的地址（默认 `http://localhost:8501`）即可开始创作。

## 🔧 环境变量

| 变量 | 是否必填 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `DEEPSEEK_API_KEY` | ✅ 必填 | — | 大模型服务 API Key，不写入代码或页面 |
| `DEEPSEEK_BASE_URL` | 选填 | `https://api.deepseek.com/v1` | OpenAI 兼容接口地址 |
| `DEEPSEEK_MODEL` | 选填 | `deepseek-chat` | 调用的模型名称 |

> 本地开发放在 `.env`；部署到 Streamlit Cloud 时在 **Settings → Secrets** 中按相同键名配置即可。

## ⚠️ 免责声明

生成内容由大模型根据用户设定产出，仅供创作参考；请自行核对情节、人物与合规性，不要直接照搬受版权保护的作品。
