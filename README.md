# SideStore 简体中文版

> 无需越狱、由社区驱动的 iOS 侧载应用商店 —— **全量简体中文汉化版**
>
> **汉化：東't-Move** ｜ 上游项目：[SideStore/SideStore](https://github.com/SideStore/SideStore) ｜ 许可：AGPL-3.0

[![最新发布版](https://img.shields.io/github/v/release/SheldonJoO/SideStore-zh-Hans?label=最新汉化版&color=blue)](https://github.com/SheldonJoO/SideStore-zh-Hans/releases/latest)
[![下载 IPA](https://img.shields.io/badge/下载-SideStore--zh--Hans.ipa-green)](https://github.com/SheldonJoO/SideStore-zh-Hans/releases/latest)
[![许可](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

本项目在保持上游 SideStore 全部功能与代码结构不变的前提下，**仅新增简体中文语言资源**（`zh-Hans.lproj`），把英文界面全量汉化为简体中文。未改动任何一行业务逻辑。

---

## 📦 下载与安装

### 方式一：下载预编译汉化包（推荐）

前往 **[Releases 页面](https://github.com/SheldonJoO/SideStore-zh-Hans/releases/latest)** 下载 `SideStore-zh-Hans.ipa`。

> ⚠️ 汉化 IPA **未签名**，和官方 Release 一样，需要你用自己的 Apple ID 重新签名后才能安装。

三种安装方式任选其一：

1. **用已安装的 SideStore 自行安装**：把 `SideStore-zh-Hans.ipa` 拷到设备的「文件」App，用 SideStore 导入安装即可覆盖 / 并存安装。
2. **用 AltServer / SideServer**：连上电脑，拖入 IPA 签名安装。
3. **用其他签名工具**（如 Sideloadly、esigntool、Xcode）自行签名安装。

首次安装后仍需按 SideStore 常规流程：登录 Apple ID、导入配对文件（pairing file），然后才能安装或刷新应用。

### 方式二：从源码自行编译

本工程保留 Xcode 的「文件系统同步组」，新增的 `.lproj` 资源在磁盘上即可被自动收录，**无需手动改 Products / Build Phases**。

```bash
git clone https://github.com/SheldonJoO/SideStore-zh-Hans.git SideStore-zh
cd SideStore-zh
git submodule update --init --recursive
# 参考上游 CodeSigning.xcconfig.sample 配置 CodeSigning.xcconfig
open AltStore.xcodeproj
```

编译要求与上游一致：Xcode 15+、iOS 14+ 目标、Rustup（`brew install rustup`）。把设备或模拟器的系统语言设为「简体中文」即可看到中文界面。

---

## 🌏 汉化覆盖范围

| 项目 | 数量 / 范围 | 说明 |
| --- | --- | --- |
| 主应用界面文案 | **1364 条** | `Localizable.strings`，含补全的 197 条缺失文案（118 条 SwiftUI 字面量 + 79 条 `NSLocalizedString`），按 IPA 实际构建提交 `6032424a` 提取对齐 |
| 界面构建器（storyboard / xib） | 4 个 storyboard + 7 个 xib | `Main`、`Settings`、`Sources`、`Authentication` 四个 storyboard 与 7 个 xib，**已用 `ibtool` 编译为 `*.storyboardc` / `*.nib` 并随 IPA 发布**（早期版本仅写入未编译的 `.strings`，运行时不生效，本次已修复） |
| 系统授权说明（purpose string） | `InfoPlist.strings` | 如本地网络权限说明等 |
| 桌面组件文案 | 13 条 | 「我的应用」小组件 |
| 标签页 / 导航 | 全中文化 | 浏览、资讯、来源、我的应用、设置 等 |

文案通过静态分析 Swift 源码中的 `NSLocalizedString` 与 SwiftUI `Text` / `Button` / `Label` 等构造器字面量提取；插值串（如 `%@`、`%lld`）按 SwiftUI `LocalizedStringKey` 的生成规则还原为对应占位符，保证格式化参数类型一致。

---

## ⚠️ 已知限制

- **资讯（News）流内容来自远程源**：`News` 标签页的文章标题 / 摘要由来源服务器（默认 `https://sidestore.io/default-sources` 及各「来源」自行下发的 RSS）提供，App 内无法汉化，始终为来源语言。这是上游设计，并非汉化遗漏 —— 切换系统语言不会改变资讯内容。
- **专有名称保持原样**：`SideStore`、`LocalDevVPN`、`Anisette`、`MACDIRTYCOW`、`SideJITServer`、patreon 昵称等品牌 / 技术词，以及开源软件许可正文，按行业惯例保留英文。格式占位符（`%@` 等）、密码掩码、示例占位文本同理。
- **随包内置的 `SideBackup.ipa`**：该备份辅助 App 的界面文案编译进了二进制、无独立语言资源文件，本汉化包未重编译其二进制，故其内部界面仍为英文（源码已提供对应中文资源，自行编译时生效）。
- 极个别运行时动态拼接、无法还原为固定 localization key 的文案可能仍显示英文，不影响功能。

---

## 📄 署名与许可

- 上游版权归 **SideStore Team** 及各自贡献者所有，本项目沿用上游 **AGPL-3.0** 许可，详见 `LICENSE`。
- **简体中文汉化：東't-Move**，汉化资源仍在同一 AGPL-3.0 许可下发布。
- 本仓库仅为方便中文用户使用的非官方汉化分发，与 SideStore 官方团队无隶属关系。

---

*English documentation of the upstream project: [SideStore/SideStore](https://github.com/SideStore/SideStore#readme).*
