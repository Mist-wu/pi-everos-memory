<p align="center">
    <h1 align="center">✨ Personal OS ✨</h1>
    <p align="center">
        个人 AI 协作系统 · A personal AI collaboration system
    </p>
</p>

以「我与 [pi](https://github.com/earendil-works/pi) agent 的对话」为入口，用 [EverOS](https://everos.evermind.ai) 做长期记忆层，
让 agent 在持续对话中越来越了解我，并扮演研究员、助教、程序员助手、秘书、编辑、复盘教练等角色。

## 核心构成

- **入口**：与 pi agent 的日常对话，不依赖 Markdown 知识库。
- **记忆层**：EverOS 云端服务自动抽取结构化记忆、维护用户画像、消解矛盾。
- **接入方式**：纯 TypeScript 的 pi 扩展包 `pi-everos-memory`（`.pi/extensions/everos-memory/`），
  通过 `fetch` 直连 EverOS REST API，注册 9 个模型可调用工具。

### 工具一览

| 类别 | 工具 |
| --- | --- |
| User 记忆 | `memory_search` · `memory_add` · `memory_profile` · `memory_episodes` · `memory_foresight` · `memory_delete` |
| Agent 记忆 | `agent_skills` · `agent_cases` · `agent_record` |

- 是否记入由 agent 判断，不每轮强制写入。
- 纠正事实优先 `memory_add`（EverOS 自动消解矛盾顶替旧画像），真要抹除才 `memory_delete`。

## 快速开始

1. 在 <https://everos.evermind.ai> 申请 API Key，写入仓库根 `.env`（已被 `.gitignore`，不提交）：

   ```
   EVEROS_API_KEY="<your_key>"
   ```

2. 按 [pi package 规范](https://github.com/earendil-works/pi/tree/main/packages/coding-agent/docs/packages.md)安装扩展（本地路径源，源码仍留在仓库）：

   ```bash
   pi install "$PWD/.pi/extensions/everos-memory"   # 用户级，全机生效
   # 或 pi install -l ./.pi/extensions/everos-memory # 项目级，随仓库共享
   ```

   `pi list` 查看已装包，`pi remove <source>` 卸载，`pi config` 启用/禁用单项资源。

3. 启动 pi，正常对话即可——agent 会按需 `memory_search` / `memory_add`。

## 文档

- [`docs/everos.md`](docs/everos.md)：EverOS 记忆层设计、工具说明、配置与接入。
- [`TODO.md`](TODO.md)：路线图与设计原则。
- [`.pi/extensions/everos-memory/README.md`](.pi/extensions/everos-memory/README.md)：扩展包说明。

## 设计原则

- 单用户、个人使用，`user_id` 固定 `wu`。
- 记忆存储交给 EverOS，不再维护 Markdown 知识库。
- 人定方向、做关键决策与审核；AI 负责检索、总结、草稿、初步分析。

## 交流

- Pull Request
- Issue
- Wechat: qbsdw0616
