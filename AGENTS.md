# AGENTS.md

本文件面向在此仓库工作的 AI 编码助手。

## 项目概述

- 《逃离鸭科夫》(Escape from Duckov) 官方 modding 示例仓库：一份 README 规则说明 + 一个最小示例 mod `DisplayItemValue`（悬停物品时显示其价值）。
- 本仓库 `ducky7go/duckov_modding` 是 fork。本地只配置了 `origin`，未配置 upstream（`xvrsl/duckov_modding`），无法在本地核对与原仓库的代码差异。fork 自身的改动包括 README 的“社区贡献 / Ducky.Sdk”一节（提交 `e753a5d`）。
- 文档语言：`README.md` 为中文主文档，另有 `README_EN.md`、`README_KO.md`。改动 README 时请三个语言版本保持同步。

## 目录结构

- `README.md` / `README_EN.md` / `README_KO.md`：mod 加载规则（info.ini 的 `name` 即命名空间，`<name>.ModBehaviour` 继承 `Duckov.Modding.ModBehaviour`）、文件夹结构、csproj 配置、创意工坊 Tags、社区准则。
- `DisplayItemValue/`：示例 mod 源码（`ModBehaviour.cs`、`DisplayItemValue.csproj`、`DisplayItemValue.sln`、`.gitignore`）。`DisplayItemValue/ReleaseExample/DisplayItemValue/` 是已发布形态示例（`DisplayItemValue.dll` + `info.ini` + `preview.png`）。
- `DisplayItemValue.sln`（仓库根）：解决方案；`.vscode/settings.json` 的 `dotnet.defaultSolution` 指向它。`DisplayItemValue/` 下另有一份 `DisplayItemValue.sln`。
- `Documents/NotableAPIs.md`、`Documents/NotableAPIs_CN.md`：值得注意的游戏 API（物品生成、本地化等）。
- `Extra/Shaders/`：`SodaCharacter.shader`、`SodaLit.shader`。
- `UnityFiles/manifest.json`：用 Unity 开发时可参考的 package 清单。

## 构建 / 运行

- 目标框架 `netstandard2.1`，`Nullable` 开启；README 提示 `netstandard2.1` 不支持 `<ImplicitUsings>`，需删除。
- 工程通过 `DuckovPath` 引用本机游戏的 `Duckov_Data\Managed\` 下的 `TeamSoda.*`、`ItemStatsSystem.dll`、`Unity*`（mac 通过 `SubPath` 使用 `/Duckov.app/Contents/Resources/Data/Managed/`）。`DisplayItemValue.csproj` 里的 `DuckovPath` 是示例占位路径（Windows：`E:\Program Files (x86)\Steam\...`，mac：`/Users/Somebody/...`），构建前需改成本机安装路径，不要把个人路径提交回来。没有游戏安装就无法编译。
- 仓库没有测试和 CI。本地测试方式：把 mod 文件夹（dll + `info.ini` + `preview.png`）放进游戏的 `Duckov_Data/Mods`。
- `info.ini` 字段：`name`、`displayName`、`description`、`publishedFileId`、`tags`。上传创意工坊时游戏会改写该文件，所以不要在里面存别的信息（README 的警告）。

## 约定

- 这是上游教学/示例仓库，改动应保持最小：修正文档、同步多语言 README、更新示例即可，不要引入框架或大范围重构。
- 示例代码风格：命名空间块（非 file-scoped）、4 空格缩进，与现有 `ModBehaviour.cs` 保持一致。
- 提交信息：fork 的历史是 `docs: ...` 风格（如 `docs: Adds Ducky.Sdk to community contributions`）。

## 注意事项

- `DisplayItemValue/ReleaseExample/DisplayItemValue/DisplayItemValue.dll` 是已提交的二进制，不要手工修改或重新生成后提交，除非确实要更新示例发布包。
- `DisplayItemValue.csproj` 带 UTF-8 BOM。README 提示：若 IDE 报路径无法识别，需把文件编码由 UTF-8 with BOM 改为 UTF-8（无 BOM）后保存。
- `README.md` 的 Tags 列表末尾有一个孤立的 `- ` 空项（上游遗留）。
- 社区贡献一节推荐 `Ducky.Sdk`（NuGet）与 `ducky7go/Ducky.Samples`；该节内容为非官方并带免责声明，修改时保留免责声明。
