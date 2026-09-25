# Jev 聊天助手 · WeKit 版

适配 **WeKit**（`Ujhhgtg/WeKit`）微信模块的 Java/BeanShell 脚本。对方私聊发消息后，本地立刻判断意图 / 危险等级 / 情绪；可选接入**任意 OpenAI 兼容大模型**（小米 MiMo、DeepSeek、通义、智谱、OpenAI 等）给出建议和 3 条候选回复，候选自动复制到剪贴板，**手动粘贴发送，绝不自动发消息**。

> 本项目**只适配 WeKit 模块**。把整个文件夹放到 `<模块数据>/scripts_java/<任意目录名>/` 下，在 WeKit 设置 → 功能 → 脚本 (Java) 里启用。
>
> 同系列：
> - WA (WAuxiliary) 版：`kongbai006/jev-wa-mimo`
> - QStory 版：`kongbai006/jev-qstory-mimo`
> - Nuke 版：`kongbai006/jev-nuke-mimo`

## 安装

1. 从 Release 下载 `Jev聊天助手WeKit_vX.X.zip`；
2. 解压，把里面的 `main.java` + `info.prop` 放到 WeKit 的 `scripts_java/jev/` 目录；
3. 打开 WeKit → 功能 → 脚本 (Java)，启用「Jev聊天助手WeKit版」；
4. 进入要分析的微信私聊，聊天框输入 `/jev` 打开配置页；
5. 点「开启本会话」；
6. （可选）打开「接入大模型决策」，填 API 地址 / 密钥 / 模型。

## 配置项（聊天框输入 `/jev`）

| 配置项 | 说明 |
| --- | --- |
| 作用域 | 开启/关闭当前会话，同时只开一个 |
| 自动分析对方消息 | 总开关 |
| 接入大模型决策 | 关=只本地秒判；开=再调大模型出建议+候选 |
| API 密钥 | 任意厂商 `sk-` 密钥，默认空 |
| API 地址 | OpenAI 兼容 `/v1` 地址；默认 MiMo `https://api.xiaomimimo.com/v1` |
| 模型 | 默认 `mimo-v2.6-flash`，可改成 `deepseek-chat` / `qwen-plus` 等 |
| 关系描述 | 默认「对方是我的关系亲密的对象」 |
| 上下文轮数 | 0–30，取最近 N 条历史辅助判断，0=不取 |
| 排版宽度 | 系统消息补全角空格宽度，0=自动 |

## 常见厂商填法

| 厂商 | API 地址 | 模型示例 |
| --- | --- | --- |
| 小米 MiMo（默认） | `https://api.xiaomimimo.com/v1` | `mimo-v2.6-flash` |
| DeepSeek | `https://api.deepseek.com/v1` | `deepseek-chat` |
| 阿里通义 | `https://dashscope.aliyuncs.com/compatible-mode/v1` | `qwen-plus` |
| 智谱 | `https://open.bigmodel.cn/api/paas/v4` | `glm-4-flash` |
| OpenAI | `https://api.openai.com/v1` | `gpt-4o-mini` |

## 行为说明

- 只分析单人私聊，群聊忽略；
- 情绪分 开心 / 难过 / 生气，无匹配显示「平静」；
- 候选回复**不会自动发**，自动复制到系统剪贴板，微信输入框长按粘贴后挑一条发；
- 判断结果仅供娱乐参考，本工具不绕过任何平台安全机制。

## 解压目录说明（重要）

**不要**把 zip 里的文件直接散着解压到模块的脚本根目录。模块是按「一个子文件夹 = 一个脚本」来识别的：

```
<脚本根目录>/
├── jev/                  ← 这个文件夹叫什么，脚本列表里就显示什么名字
│   ├── info.prop         ← 该脚本的全部文件都放在这个子文件夹里
│   ├── main.java
│   └── readme.md（可选）
├── 另一个脚本/
│   └── ...
└── ...
```

- 文件夹名就是脚本在列表里的显示名，可以随便起；
- 模块只扫描脚本根目录下的一层子文件夹，不会递归进更深的目录；
- 直接把 `main.java`、`info.prop` 散在脚本根目录下是**识别不出来**的。
