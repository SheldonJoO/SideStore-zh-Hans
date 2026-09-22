# SideStore 简体中文版

> SideStore 简体中文汉化版 —— 无需越狱、由社区驱动的 iOS 应用商店
>
> **汉化：東't-Move** ｜ 上游项目：[SideStore/SideStore](https://github.com/SideStore/SideStore)

本项目在保持上游 SideStore 全部功能与代码结构不变的前提下，**仅新增简体中文语言资源**（`zh-Hans.lproj`），把英文界面全量汉化为简体中文。

## 内容清单

| 项目 | 位置 | 说明 |
| --- | --- | --- |
| 预编译汉化包 | `SideStore-zh-Hans.ipa` | 基于官方 0.7.0-alpha，已内置中文资源，见下方安装说明 |
| 主应用汉化资源 | `AltStore/zh-Hans.lproj/` | Localizable.strings、各 storyboard / xib 译文、InfoPlist.strings |
| 桌面组件汉化资源 | `AltWidget/zh-Hans.lproj/` | 「我的应用」小组件文案 |
| SideBackup 汉化资源 | `SideBackup/zh-Hans.lproj/` | 备份 / 恢复辅助 App 文案 |
| 工程配置 | `AltStore.xcodeproj`、`*/Info.plist` | `knownRegions` 与 `CFBundleLocalizations` 加入 `zh-Hans` |

## 汉化覆盖范围

- 主应用界面文案：**1185 条**（`Localizable.strings` 实际写入 1160 条，重复的 %@ 占位符、纯数值等未重复写入）
- 界面构建器（storyboard / xib）文案：**111 条**，覆盖 `Main`、`Settings`、`Sources`、`Authentication`、`AppBannerView`、`SourceHeaderView`、`SettingsHeaderFooterView`、`AboutPatreonHeaderView`、`InstalledAppsCollectionHeaderView`、`UpdateCollectionViewCell`
- 系统授权说明、应用 purpose string：`InfoPlist.strings`
- 桌面组件文案：**13 条**

文案通过静态分析 Swift 源码中的 `NSLocalizedString` 与 SwiftUI `Text` / `Button` / `Label` 等构造器字面量提取，插值串（如 `%@`、`%lld`）按 SwiftUI `LocalizedStringKey` 的生成规则还原为对应占位符，保证格式化参数类型一致。

## 安装汉化 IPA

**前提条件**：汉化 IPA **未签名**，和官方 Release 一样，需要你用自己的 Apple ID 重新签名后才能安装。

三种方式任选其一：

1. **用已安装的 SideStore 自行安装**：把 `SideStore-zh-Hans.ipa` 拷到设备的「文件」App，用 SideStore 导入安装即可覆盖 / 并存安装。
2. **用 AltServer / SideServer**：连上电脑，拖入 IPA 签名安装。
3. **用其他签名工具**（如 Sideloadly、esigntool、Xcode）自行签名安装。

首次安装后仍需按 SideStore 常规流程：登录 Apple ID、导入配对文件（pairing file），然后才能安装或刷新应用。

> 提示：由于 SideStore 自身的签名证书到期或团队信息变化可能导致重签提示，请以 SideStore 提示为准（「立即重签 / 稍后重签」）。

## 从源码自行编译

本工程保留 Xcode 16 的「文件系统同步组」，新增的 `.lproj` 资源在磁盘上即可被自动收录，**无需手动改 Products / Build Phases**。

```bash
git clone <本仓库地址> SideStore-zh
cd SideStore-zh
# 按上游说明初始化子模块与依赖
git submodule update --init --recursive
# 参考上游 CodeSigning.xcconfig.sample 配置 CodeSigning.xcconfig
open AltStore.xcodeproj
```

编译要求与上游一致：Xcode 15+、iOS 14+ 目标、Rustup（`brew install rustup`）。
把设备或模拟器的系统语言设为「简体中文」即可看到中文界面。

## 已知限制

- 部分**运行时动态拼接**的文案仍需英文：源码中有少量 `NSLocalizedString("\\(变量) …")` 写法，运行时 key 是拼接后的结果，静态 .strings 无法命中。
- 少量富 ternary 插值（如 `Text("Tap toggle to view \\(flag ? "bundle" : "resigned") profile")`）未收录。
- 专有名称（如 SideStore、LocalDevVPN、Anisette、patreon 昵称等）与 IB 中的示例占位文本保持原样。
- 随包内置、上游预编译的 `SideBackup.ipa` 二进制本身未重编译，其内部界面仍为英文（源码已提供中文资源，自行编译时生效）。
- 汉化文案基于开发分支提取，与官方 Release 二进制存在少量版本漂移，未命中的条目会回退英文显示，不影响功能。

## 署名与许可

- 上游版权归 **SideStore Team** 及各自贡献者所有，本项目沿用上游 **AGPL-3.0** 许可，详见 `LICENSE`。
- **简体中文汉化：東't-Move**，汉化资源仍在同一 AGPL-3.0 许可下发布。
- 本仓库仅为方便中文用户使用的非官方汉化分发，与 SideStore 官方团队无隶属关系。

---

*本 README 为汉化项目的中文说明，上游原始说明请见 [README.md](README.md)。*
