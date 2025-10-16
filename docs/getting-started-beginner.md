# Qwen Code 新手入门指南（Step by Step）

> 这份指南假设你完全没有经验，按顺序完成即可逐步搭建并熟悉 Qwen Code 的开发环境。

## 1. 准备开发环境

1. **安装 Node.js 20**  
   - 推荐直接访问 [Node.js 官网](https://nodejs.org/) 下载 `LTS` 版本（20.x）。  
   - 安装完成后，打开终端执行 `node -v` 与 `npm -v` 确认版本。
2. **安装 Git（如未安装）**  
   - macOS 使用 `brew install git`，Windows 可以在 [Git 官网](https://git-scm.com/) 下载安装包，Linux 使用发行版的包管理器。  
   - 运行 `git --version` 确认安装成功。

> ✅ 如果你不确定命令在哪执行，只需打开系统自带终端（Windows 建议使用 "Git Bash" 或 "Windows Terminal"）。

## 2. 克隆并进入项目

```bash
# 下载仓库
git clone https://github.com/QwenLM/qwen-code.git

# 进入仓库目录
cd qwen-code
```

> 如果 Git 下载速度慢，可选择使用镜像源或在 GitHub 上下载 ZIP 压缩包后手动解压。

## 3. 安装依赖

```bash
npm install
```

- 第一次安装会比较慢，因为会下载所有依赖包。  
- 若网络受限，可以配置 npm 国内镜像：`npm config set registry https://registry.npmmirror.com`。

## 4. 初次体验 CLI

1. **本地直接运行源码：**
   ```bash
   npm start
   ```
   - 终端会出现 `qwen>` 提示符，说明 CLI 已启动。  
   - 输入 `/help` 可以查看支持的基础指令。
2. **先感受功能：** 在 CLI 中输入类似 “介绍一下这个项目” 或 “帮我生成一个 README 模板” 的请求，熟悉交互方式。

## 5. 配置免费模型额度

1. 首次运行时，CLI 会引导你选择登录方式。  
2. 推荐使用 **Qwen OAuth**：按照终端提示在浏览器中登录 qwen.ai 账号即可。  
3. 如果你在国内，可以在设置中选择 ModelScope；在海外则可选择 OpenRouter 的免费额度。

> 登录成功后，CLI 会把认证信息保存到 `~/.qwen/credentials.json`，后续无需重复登录。

## 6. 常用开发命令

| 场景 | 命令 | 说明 |
| --- | --- | --- |
| 构建全部包 | `npm run build` | 首次或修改核心代码后运行，确保编译通过 |
| 运行单元测试 | `npm run test` | 检查关键逻辑是否正常 |
| 进行端到端测试 | `npm run test:e2e` | 验证 CLI 的整体流程 |
| 一键预检 | `npm run preflight` | 包含 lint、格式化、构建、测试等全量校验 |

> 新手阶段建议在每次提交代码前执行 `npm run test` 或 `npm run preflight`，可以提前发现问题。

## 7. 了解代码结构

1. 打开 `packages/cli/src/index.ts`：了解 CLI 如何启动和读取配置。  
2. 打开 `packages/core/src/index.ts`：认识核心逻辑如何组合模型调用与工具。  
3. 阅读 `docs/architecture.md` 与 `docs/cli/overview.md`：配合源码一起理解整体架构。

> 提示：使用 VS Code 等编辑器时，按住 `Ctrl`（macOS 为 `Cmd`）点击函数名即可跳转到定义，便于快速熟悉代码。

## 8. 从首个小任务入手

1. 在仓库中创建一个新分支，例如 `git checkout -b feat/my-first-change`。  
2. 根据兴趣选择一个切入点：
   - 想改进 CLI 交互 → 关注 `packages/cli` 下的 UI 组件或命令解析。  
   - 想扩展工具能力 → 查看 `packages/core/src/tools` 及其注册方式。  
   - 想了解多模态能力 → 参考 `docs/vision.md` 和相关配置文件。
3. 修改代码后运行测试，确保没有报错。
4. 使用 `git status` 查看变更，`git diff` 检查修改内容。

## 9. 提交与贡献

1. 提交前请阅读 [`CONTRIBUTING.md`](../CONTRIBUTING.md)，了解代码风格和提交流程。  
2. 使用 `git commit -am "feat: 描述你的改动"` 提交（首次提交需要先 `git add` 变更文件）。  
3. 在 GitHub 上创建 Pull Request，描述改动内容、测试情况以及使用场景。

## 10. 常见问题排查

| 症状 | 排查步骤 |
| --- | --- |
| `npm install` 报网络错误 | 检查代理/防火墙，或切换到国内镜像源 |
| CLI 启动后无法调用模型 | 确认登录方式是否成功，或执行 `/auth` 重新登录 |
| 构建失败 | 查看终端日志中的错误文件，根据提示修复 TypeScript/依赖问题 |
| 测试报错 | 使用 `npm run test -- --runInBand --watch` 逐个定位失败用例 |

> 如果仍无法解决，可在 Issue 中附上日志截图和复现步骤，寻求社区帮助。

---

按照上述步骤逐项完成，你就能在本地成功运行 Qwen Code，理解其核心结构，并为后续功能开发打下基础。祝你上手顺利！
