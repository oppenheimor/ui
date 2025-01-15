# 贡献指南

感谢您有兴趣为 ui.shadcn.com 做出贡献。我们很高兴有您的参与。

在提交您的第一个拉取请求之前，请花点时间阅读本文档。我们也强烈建议您查看已开启的 issues 和拉取请求，看看是否有人正在进行类似的工作。

如果您需要任何帮助，欢迎联系 [@shadcn](https://twitter.com/shadcn)。

## 关于仓库

这是一个多包仓库。

- 我们使用 [pnpm](https://pnpm.io) 和 [`workspaces`](https://pnpm.io/workspaces) 进行开发
- 我们使用 [Turborepo](https://turbo.build/repo) 作为构建系统
- 我们使用 [changesets](https://github.com/changesets/changesets) 来管理发布

##  结构

仓库结构如下。

```
apps
└── www
    ├── app
    ├── components
    ├── content
    └── registry
        ├── default
        │   ├── example
        │   └── ui
        └── new-york
            ├── example
            └── ui
packages
└── cli
```

| 路径                  | 描述                              |
| --------------------- | ---------------------------------------- |
| `apps/www/app`        | 网站的 Next.js 应用程序。 |
| `apps/www/components` | 网站的 React 组件。    |
| `apps/www/content`    | 网站的内容。             |
| `apps/www/registry`   | 组件的注册表。         |
| `packages/cli`        | `shadcn-ui` 包。                 |

## 开发

### Fork 仓库

您可以通过点击本页面右上角的 fork 按钮来 fork 此仓库。

### Clone 到你本地的机器上

```bash
git clone https://github.com/your-username/ui.git
```

### 进入项目目录

```bash
cd ui
```

### 创建新分支

```bash
git checkout -b my-new-branch
```

### 安装依赖

```bash
pnpm install
```

### 运行 workspace 工作区

可以使用 `pnpm --filter=[WORKSPACE]` 命令来启动工作区的开发过程。

#### 示例

1. 运行 `ui.shadcn.com` 网站:

```bash
pnpm --filter=www dev
```

2. 运行 `shadcn-ui` 包：

```bash
pnpm --filter=shadcn-ui dev
```

## 本地运行

要在本地运行，可以按照以下工作流进行操作：

1. 首先运行注册表（主站点），以确保组件是最新的：

   ```bash
   pnpm www:dev
   ```

2. 运行开发脚本：

   ```bash
   pnpm shadcn:dev
   ```

3. 在另一个终端 tab 中，通过运行以下命令来测试：

   ```bash
   pnpm shadcn
   ```

   要在特定应用程序中测试命令，请使用以下命令：

   ```bash
   pnpm shadcn <init | add | ...> -c ~/Desktop/my-app
   ```

4. 运行测试：

   ```bash
   pnpm --filter=shadcn test
   ```

此工作流程确保您在本地环境中运行的是注册表的最新版本，并正确测试了命令。

## 文档

本项目的文档位于 `www` 工作区中。您可以通过运行以下命令来本地运行文档：

```bash
pnpm --filter=www dev
```

文档使用 [MDX](https://mdxjs.com) 编写。您可以在 `apps/www/content/docs` 目录中找到文档文件。

## 组件

我们使用注册系统来开发组件。您可以在 `apps/www/registry` 下找到组件的源代码。组件按照样式进行组织。

```bash
apps
└── www
    └── registry
        ├── default
        │   ├── example
        │   └── ui
        └── new-york
            ├── example
            └── ui
```

在添加或修改组件时，请确保：

1. 对每种样式进行更改。
2. 更新文档。
3. 运行 `pnpm build:registry` 更新注册表。

## 提交约定

在创建 Pull Request 之前，请检查您的提交是否符合
本仓库使用的提交约定。

当您创建提交时，我们请您在提交信息中遵循
`category(scope or module): message` 的约定，并使用以下之一的类别：

- `feat / feature`: 引入完全新代码或新特性的所有更改
- `fix`: 修复错误的更改（如果存在，理想情况下您还会引用相关的问题）
- `refactor`: 任何与代码相关的更改，不是修复也不是特性
- `docs`: 更改或创建新的文档（例如README、库或CLI使用文档）
- `build`: 软件构建的所有更改，包括对依赖项的更改或添加新的依赖项
- `test`: 测试的所有更改（添加新测试或更改现有测试）
- `ci`: 连续集成配置的所有更改（例如github actions、ci系统）
- `chore`: 不属于上述任何类别的仓库更改

例如：`feat(components): add new prop to the avatar component`

如果您对详细规范感兴趣，可以访问
https://www.conventionalcommits.org/ 或查看
[Angular提交信息指南](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)。

## 新组件请求

如果您有新的组件请求，请在 GitHub 上开启讨论。我们将很高兴帮助您。

## CLI

`shadcn-ui` 包是一个用于向项目添加组件的 CLI。您可以在[这里](https://ui.shadcn.com/docs/cli)找到 CLI 的文档。

对 CLI 的任何更改都应在 `packages/cli` 目录中进行。如果可能，添加测试来验证您的更改将是非常有益的。

## 测试

测试使用[Vitest](https://vitest.dev)编写。您可以从仓库的根目录运行所有测试。

```bash
pnpm test
```

在提交 pull 请求时，请确保测试通过。如果您添加了新功能，请包含测试。
