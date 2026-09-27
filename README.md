# VASMC

[🇨🇳 中文](#zh-cn) | [🌍 English](#en)

---

<a name="zh-cn"></a>

## 🇨🇳 中文

## 退役声明：一个 AI 脚手架是怎样过期的

**项目状态：退役中。** VASMC 不再推荐用于新项目，也不再规划新功能。现有代码、包和文档保留，供已接入的项目逐步迁移；现有命令并未因此停用。

我曾认为，prompt 和 skill 值得作为软件资产管理：从源文件组合，锁定依赖，生成语言版本，并持续维护它们之间的来源与版本关系。模型会吸收通用 AI 脚手架提供的能力，本就在预期内。我高估的是，在日常使用中，长期维持这套关系能带来多少收益。

VASMC 于 2026 年 2 月创建。短短七个月后，在我的实际工作中，模型往往已经可以按项目需要形成相应的 prompt 或 skill，也可以参考已有内容，再在项目内独立维护。旧指令仍可提供帮助，但项目中的后续演化未必需要持续依附于它的源头；源头本身也可能很快停止维护或失去参考价值。此时，维持源文件、依赖、生成产物和语言版本之间的精确对应，逐渐成了一项缺少实际回报的工作。

因此，我决定停止继续扩展 VASMC。这个决定来自它在实际工作中的使用频率和维护负担。项目的意图、约束、重要历史，以及 AI 实际依据什么采取行动、改变了什么、最终被人接受了什么，仍值得认真保存。

对执行型 prompt 和 skill 而言，多语言更多服务人的阅读；但在我的实际工作中，人已很少直接阅读这些指令，预先编译语言版本也就很难带来收益。确需锁定 instruction artifact 的项目仍可使用现有版本，并在迁移时保留必要的发布检查。

参见：[AI 脚手架的半衰期](https://glenzli.com/notes/half-life-of-ai-scaffolding/)。能继续运行，不等于仍值得继续维护。

![VASMC 编译流程](docs/assets/vasmc-banner.png)

VASMC 是用于 prompt、skill 和 AI 项目文档的 Markdown 编译器。它把 `.vasm.md` 源文件展开为 `.md` 产物，并把需要继续处理的事项写入 `.vasmc/build-report.yaml`。

`@vasm/cli` 负责 import 展开、依赖锁定、语言过滤、输出路由和策略诊断等确定性工作，不调用模型。翻译、语义审查和项目上下文检查由执行构建的 AI 编辑器或开发者根据报告完成。

## 快速开始

以下命令保留供现有项目使用和迁移参考，不建议用于新项目初始化。

```bash
npm install -g @vasm/cli
vasmc init
vasmc build
```

最小源文件：

```markdown
---
vasm:
  alias: release-reviewer
  intent: "Review release notes against source changes."
  compile:
    format: executable
    targetLangs: ["en"]
---

# Release Reviewer

[Rules](./fragments/release-rules.vasm.md "@import:inline")
```

构建会生成：

- 编译后的 Markdown；
- `.vasmc/build-report.yaml`，按需列出校验、翻译、策略审查等后续事项。

`.vasm.md` 是维护入口，生成的 `.md` 是构建产物。除报告明确要求更新译文外，内容修改应回到源文件后重新构建。

## 能力边界

- `vasmc build` 不调用模型，报告中的 action 也不表示相关任务已经完成。
- 策略检查覆盖 manifest、依赖、格式边界和内容信号，不是运行时安全沙箱。
- `vasm-console` 提供可选的外部模型语义检查，与确定性编译链分开。

## 文档

| 文档 | 内容 |
| --- | --- |
| [使用手册](docs/USAGE.md) | 项目配置、构建流程和示例。 |
| [AI 工作流](docs/AI-WORKFLOW.md) | 如何处理 build report 中的 action。 |
| [协议参考](docs/REFERENCE.md) | Manifest、import、构建配置、报告和策略诊断。 |
| [CLI 帮助](HELP.md) | `vasmc` 与 `vasm-console` 命令。 |
| [设计文档](DESIGN.md) | 编译模型与设计边界。 |

## 包

| 包 | 命令 | 职责 |
| --- | --- | --- |
| `@vasm/core` | 无 | 编译器与协议实现。 |
| `@vasm/cli` | `vasmc` | 构建、依赖管理和报告生成。 |
| `@vasm/console` | `vasm-console` | 可选的外部模型 lint 与 diff。 |

## 开发与发布

```bash
npm install
npm test
npm run build
npm run release:check
npm run release -- --dry-run
```

`npm run release` 默认发布到 npmjs、GitHub 和 GitLab。可使用 `--only` 选择目标，或使用 `--skip` 排除目标。

---

<a name="en"></a>

## 🌍 English

## Retirement notice: How an AI scaffold became obsolete

**Project status: retiring.** VASMC is no longer recommended for new projects, and no new features are planned. Existing code, packages, and documentation remain available while current users migrate; existing commands have not been disabled.

I once thought prompts and skills were worth managing as software assets: composing them from source files, pinning dependencies, generating language variants, and maintaining their provenance and version relationships over time. I already expected models to absorb the capabilities supplied by general AI scaffolding. What I overestimated was the practical return from maintaining those relationships over the long term.

VASMC began in February 2026. Just seven months later, in my actual work, models can often form the prompt or skill a project needs, or consult existing material and then maintain their own versions within the project. Older instructions can still help, but subsequent changes within a project need not remain tied to the original source; that source may itself quickly stop being maintained or lose its relevance. Maintaining precise relationships between source files, dependencies, generated outputs, and language variants has gradually become work with little practical return.

I have therefore decided to stop expanding VASMC. This decision reflects how often it is used and the effort required to maintain it in my actual work. Project intent, constraints, important history, and what AI actually based its actions on, what it changed, and what people ultimately accepted still deserve careful preservation.

For executable prompts and skills, multiple languages mainly serve human readers; in my actual workflow, people rarely read those instructions directly anymore, so precompiled language variants add little value. Projects that need pinned instruction artifacts can continue using the existing version and retain the release checks they need during migration.

See [The Half-Life of AI Scaffolding](https://glenzli.com/en/notes/half-life-of-ai-scaffolding/). A tool can still run without being worth continued maintenance.

![VASMC compile flow](docs/assets/vasmc-banner.png)

VASMC is a Markdown compiler for prompts, skills, and AI project documentation. It expands `.vasm.md` source files into `.md` output and records follow-up work in `.vasmc/build-report.yaml`.

`@vasm/cli` performs deterministic work such as import expansion, dependency locking, language filtering, output routing, and policy diagnostics. It does not call a model. Translation, semantic review, and project-context checks are completed by the AI editor or developer running the build, based on the report.

## Quick Start

These commands remain for existing projects and migration reference. Starting a new project with VASMC is no longer recommended.

```bash
npm install -g @vasm/cli
vasmc init
vasmc build
```

Minimal source:

```markdown
---
vasm:
  alias: release-reviewer
  intent: "Review release notes against source changes."
  compile:
    format: executable
    targetLangs: ["en"]
---

# Release Reviewer

[Rules](./fragments/release-rules.vasm.md "@import:inline")
```

The build produces:

- Compiled Markdown;
- `.vasmc/build-report.yaml`, listing follow-up verification, translation, or policy-review work when needed.

`.vasm.md` is the maintenance surface; generated `.md` files are build output. Unless the report explicitly asks for a translation update, edit the source and rebuild.

## Boundaries

- `vasmc build` does not call a model, and an action in the report does not mean that work has been completed.
- Policy checks cover manifests, dependencies, format boundaries, and content signals. They are not a runtime security sandbox.
- `vasm-console` provides optional external-model checks and remains separate from the deterministic compiler path.

## Documentation

| Document | Contents |
| --- | --- |
| [Usage Guide](docs/USAGE.md) | Project configuration, build workflow, and examples. |
| [AI Workflow](docs/AI-WORKFLOW.md) | How to handle actions in the build report. |
| [Protocol Reference](docs/REFERENCE.md) | Manifests, imports, build configuration, reports, and policy diagnostics. |
| [CLI Help](HELP.md) | Commands for `vasmc` and `vasm-console`. |
| [Design](DESIGN.md) | Compiler model and design boundaries. |

## Packages

| Package | Command | Role |
| --- | --- | --- |
| `@vasm/core` | none | Compiler and protocol implementation. |
| `@vasm/cli` | `vasmc` | Builds, dependency management, and report generation. |
| `@vasm/console` | `vasm-console` | Optional external-model lint and diff commands. |

## Development and release

```bash
npm install
npm test
npm run build
npm run release:check
npm run release -- --dry-run
```

`npm run release` publishes to npmjs, GitHub, and GitLab by default. Use `--only` to select targets or `--skip` to exclude them.
