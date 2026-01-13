<div align="center">
  <h1>
    ✨ 人格引擎 <img src="./assets/dance.webp" width="30px" alt="跳舞吉祥物"> ✨
  </h1>

  <p><i>借助AI驱动的语音、动画和人格魅力，释放你的数字角色无限潜能！</i></p>

<p>
  <a href="https://github.com/fagenorn/handcrafted-persona-engine/releases/latest" target="_blank"><img alt="GitHub 下载量（所有资源，所有版本）" src="https://img.shields.io/github/downloads/fagenorn/handcrafted-persona-engine/total?style=for-the-badge&logo=github"></a>
  &nbsp;&nbsp; <a href="https://discord.gg/p3CXEyFtrA" target="_blank"><img alt="Discord" src="https://img.shields.io/discord/1347649495646601419?style=for-the-badge&logo=discord&logoColor=white&label=Discord&color=5865F2"></a>
  &nbsp;&nbsp; <a href="https://x.com/fagenorn" target="_blank"><img alt="X（原Twitter）关注数" src="https://img.shields.io/twitter/follow/fagenorn?style=for-the-badge&logo=x"></a>
</p>

  ---

  <p>
    <b>人格引擎（Persona Engine）</b> 是你的一站式交互式虚拟形象创作工具包！它巧妙融合了以下核心能力：
    <br>
    🎨 <b>Live2D：</b> 用于富有表现力的实时角色动画。
    <br>
    🧠 <b>大语言模型（LLM）：</b> 赋予角色独特的语音风格和人格特质。
    <br>
    🎤 <b>自动语音识别（ASR）：</b> 理解语音指令和日常对话。
    <br>
    🗣️ <b>文本转语音（TTS）：</b> 让角色自然开口说话。
    <br>
    🎭 <b>实时语音克隆（RVC - 可选）：</b> 模拟特定的声音特征。
    <br>
    <br>
    完美适用于 <b>虚拟主播（VTubing）🎬</b>、动态 <b>直播🎮</b> 以及创新的 <b>虚拟助手应用🤖</b> 场景。
    <br>
    <i>让你的角色前所未有地鲜活起来！</i> ✨
  </p>

  <img src="assets/header.png" alt="人格引擎" width="650">

  <h2>💖 一睹为快！💖</h2>
  <p>见证人格引擎打造的数字魔法：</p>
  <a href="https://www.youtube.com/watch?v=4V2DgI7OtHE" target="_blank"> <img src="assets/demo_1.png" alt="人格引擎演示视频" width="600"></a>
  <p><i>（点击上方图片观看演示！）</i></p>
  <br>

  <p>这是引擎更多趣味功能的简短展示：</p>
  <video src="https://github.com/user-attachments/assets/8c486a9f-db2c-4486-8e20-0b1e336e476c"></video>
  <br><br>
</div>

## 📜 目录

* [🌸 概览：引擎核心能力](#overview)
* [🚀 快速上手：安装指南](#installation-guide)
* [✨ 丰富功能一览！](#features)
* [⚙️ 架构 / 工作原理](#architecture)
* [💡 潜在应用场景](#use-cases)
* [🤝 贡献指南](#contributing)
* [🎭 Live2D 集成指南](./Live2D.md)
* [💬 加入社区！](#community)
* [❓ 支持与联系](#support)

## <a id="overview"></a>🌸 概览：引擎核心能力

人格引擎能聆听你的语音 🎤，借助强大的AI大语言模型思考 🧠（遵循你定义的人格设定！），通过合成语音回应 🔊（可选通过RVC克隆特定声音！），并驱动Live2D虚拟形象做出对应动画 🎭。

它可通过Spout协议无缝接入OBS Studio等直播软件，实现高质量视觉输出。内置的“Aria”模型经过特殊绑定优化，同时你也可以集成自定义Live2D模型（详见 [Live2D 集成指南](./Live2D.md)）。

> [!IMPORTANT]  
> 当使用**经过专属微调的大语言模型（LLM）** 时，人格引擎能实现最自然、贴合角色设定的交互效果。该模型针对引擎的专属通信格式进行了训练。
>
> 你也可以使用标准的OpenAI兼容模型（如Ollama、Groq、OpenAI提供的模型），但需要在 `personality.txt` 文件中进行精细的**提示词工程**配置。仓库中提供了模板文件（`personality_example.txt`）供你参考。
>
> **为标准模型配置 `personality.txt` 的详细说明至关重要，可参考 [安装指南](./INSTALLATION.md#configure-personality-txt---important)。**
>
> 👉 想体验微调模型或观看实时演示？加入我们的 [Discord社区](#community)！ 😊

<div align="center">
  <h3>截图展示！</h3>
  <img src="https://i.imgur.com/iQq2rxP.jpeg" alt="人格引擎与Gmail界面集成概念图" width="800">
  <br><i>作为桌面助手超实用！ 😊</i>
  <br><br>
  <img src="https://i.imgur.com/WOLMe2T.jpeg" alt="人格引擎作为AI助手运行界面" width="800">
  <br><i>窥探引擎的操控后台！ ✨</i>
  <br><br>
</div>

## <a id="installation-guide"></a>🚀 快速上手：安装指南

➡️ **请严格遵循详细的 [安装与配置指南](./INSTALLATION.md) 完成依赖安装、模型下载、参数配置和引擎运行。** ⬅️

**核心配置要求：**
* **系统：** 核心功能（ASR、TTS、RVC）**必须使用支持CUDA的NVIDIA显卡**。
* **软件：** .NET运行时、espeak-ng语音合成工具。
* **AI模型：** 下载Whisper ASR模型。
* **Live2D：** 配置Live2D模型（使用内置Aria或自定义模型）。
* **（可选）RVC：** 配置实时语音克隆功能。
* **LLM：** 配置所选大语言模型的访问方式（API密钥、接口地址）。
* **直播：** 配置Spout输出，对接OBS/其他直播软件。
* **配置：** 理解 `appsettings.json` 配置文件。
* **故障排除：** 常见问题及解决方案。

## <a id="features"></a>✨ 丰富功能一览！

<div align="center">
<img src="assets/mascot_wand.png" width="150" alt="持魔法棒的吉祥物">
</div>

* 🎭 **Live2D 虚拟形象集成：**
    * 加载并渲染Live2D模型（`.model3.json` 格式）。
    * 内置经过特殊绑定的“Aria”模型。
    * 支持基于情绪的动画（`[EMOTION:名称]` 标签）和VBridger标准唇形同步参数。
    * 提供专属的**情绪**、**待机**、**眨眼**动画服务。
    * **自定义模型开发要求详见 [Live2D 集成与绑定指南](./Live2D.md)！**

* 🧠 **AI驱动的对话交互：**
    * 对接OpenAI兼容的大语言模型（LLM）API（本地/云端均可）。
    * 由自定义的 `personality.txt` 文件定义角色人格。
    * 优化了**对话上下文管理**和**会话管理**，交互更稳定。
    * 针对可选的专属微调模型做了适配优化（见 [概览](#overview)）。

* 🗣️ **语音交互（需NVIDIA显卡）：**
    * 通过麦克风采集音频（基于 `NAudio`/`PortAudio`）。
    * 借助Silero `VAD` 检测语音片段。
    * 通过Whisper `ASR`（基于 `Whisper.NET`）识别语音内容。
    * 内置专属**插话检测**功能，更优雅地处理用户打断对话的场景。
    * 轻量快速的Whisper模型用于插话检测，更精准的大模型用于完整语音转写。

* 🔊 **高级文本转语音（TTS）（需NVIDIA显卡）：**
    * 完善的处理流程：文本标准化 → 语句分割 → 音素转换 → `ONNX` 语音合成。
    * 基于自定义 `kokoro` 语音模型实现自然语音合成。
    * 对未知词汇/符号，自动降级使用 `espeak-ng` 合成。

* 👤 **可选实时语音克隆（RVC）（需NVIDIA显卡）：**
    * 集成 `RVC` `ONNX` 模型。
    * 实时修改TTS输出语音，模拟指定目标声音。
    * 可关闭该功能以提升性能。

* 📜 **自定义字幕：**
    * 通过UI配置样式，实时显示角色语音对应的文字内容。

* 💬 **控制界面 & 聊天查看器：**
    * 专属UI窗口监控引擎运行状态。
    * 查看延迟指标（LLM响应、TTS合成、音频处理）。
    * 实时调整TTS参数（音调、语速）和轮盘互动功能设置。
    * 查看并编辑对话历史。

* 👀 **屏幕感知（实验性功能）：**
    * 可选的视觉模块，让AI能够“看到”并读取指定应用窗口的文本内容。

* 🎡 **互动轮盘（实验性功能）：**
    * 可选的可配置屏幕轮盘，增加互动趣味性。

* 📺 **直播输出（Spout协议）：**
    * 将虚拟形象、字幕、互动轮盘画面通过专属Spout流发送至OBS Studio或其他兼容软件。
    * 无需窗口捕获，支持多路可配置Spout流。

* 🎶 **音频输出：**
    * 通过 `PortAudio` 清晰播放合成语音。

* ⚙️ **配置管理：**
    * 核心配置通过 `appsettings.json` 完成（详见 [安装指南](./INSTALLATION.md#configuration-appsettingsjson)）。
    * 部分参数可通过控制界面实时调整。

* 🤬 **违禁词过滤：**
    * 基础关键词过滤 + 可选的基于机器学习（ML）的LLM回复过滤。

## <a id="architecture"></a>⚙️ 架构 / 工作原理

人格引擎通过持续循环的流程让角色“活”起来，核心步骤如下：

1.  **聆听：** 🎤
    * 麦克风采集音频信号。
    * 语音活动检测器（VAD）识别语音片段。

2.  **理解：** 👂
    * 轻量Whisper模型检测用户是否插话。
    * 语音结束后，使用更精准的Whisper模型完成完整语音转写。

3.  **上下文补充（可选）：** 👀
    * 若启用视觉模块，捕获指定应用窗口的文本内容。

4.  **思考：** 🧠
    * 将转写文本、对话历史、可选的屏幕上下文，以及 `personality.txt` 中的规则发送至配置的大语言模型（LLM）。

5.  **生成回应：** 💬
    * LLM生成文本回复。
    * 回复中可包含情绪标签（如 `[EMOTION:😊]`）或指令。

6.  **内容过滤（可选）：** 🤬
    * 对回复内容进行违禁词过滤。

7.  **语音合成：** 🔊
    * 文本转语音（TTS）系统将过滤后的文本转换为音频。
    * 优先使用 `kokoro` 语音模型。
    * 对未知内容自动降级使用 `espeak-ng`。

8.  **语音克隆（可选）：** 👤
    * 若启用实时语音克隆（RVC），实时修改TTS音频。
    * 基于ONNX模型匹配目标声音特征。

9.  **动画驱动：** 🎭
    * TTS过程中提取的音素驱动唇形同步参数（VBridger标准）。
    * LLM回复中的情绪标签触发对应的Live2D表情或动作。
    * 角色未说话时播放待机动画，保持自然状态。
    * **（详情见 [Live2D 集成与绑定指南](./Live2D.md)！）**

10. **内容展示：**
    * 📜 根据语音内容生成字幕。
    * 📺 将动画形象、字幕、可选的互动轮盘通过专属Spout流发送至OBS或其他软件。
    * 🎶 合成（并可选克隆）后的音频通过选定设备播放。

11. **循环：**
    * 引擎回到聆听状态，等待下一次交互。

<div align="center">
<br/>
<img src="assets/diagram.png" width="500" alt="架构图">
<br/>
<br/>
</div>

## <a id="use-cases"></a>💡 潜在应用场景：发挥想象！

<div align="center">
<img src="assets/mascot_light.png" width="150" alt="持灯泡的吉祥物">
</div>

* 🎬 **虚拟主播 & 直播：** 打造AI副播、响应弹幕的互动角色，甚至全AI驱动的虚拟主播。
* 🤖 **虚拟助手：** 构建个性化、带动画效果的桌面陪伴助手。
* 🏪 **互动 kiosk 终端：** 为博物馆、展会、零售场景或信息台开发沉浸式虚拟导览员。
* 🎓 **教育工具：** 设计AI语言练习伙伴、交互式历史人物问答机器人，或动态教学助手。
* 🎮 **游戏开发：** 实现更具动态性和对话能力的非玩家角色（NPC）或游戏陪伴角色。
* 💬 **角色聊天机器人：** 让用户与喜爱的虚构角色进行沉浸式对话。

## <a id="contributing"></a>🤝 贡献指南

我们热烈欢迎各类贡献！如果你有优化建议、Bug修复或新功能构想，请遵循以下步骤：

1.  **沟通（可选但推荐）：** 对于重大变更，请先在 [GitHub Issue](https://github.com/fagenorn/handcrafted-persona-engine/issues) 中讨论你的想法。
2.  **复刻仓库：** 将仓库复刻到你的GitHub账号。
3.  **创建分支：** 为你的修改创建新功能分支（`git checkout -b feature/你的功能名称`）。
4.  **开发：** 完成代码修改，尽量遵循现有编码风格，并在必要处添加注释。
5.  **提交：** 提交修改并填写清晰的提交信息（`git commit -m '新增：你的功能名称'`）。
6.  **推送：** 将分支推送到你的复刻仓库（`git push origin feature/你的功能名称`）。
7.  **创建PR：** 向原仓库的 `main` 分支提交拉取请求（Pull Request），并在PR中清晰描述修改内容。

感谢你助力人格引擎变得更好！ 😊

## <a id="community"></a>💬 加入社区！

<div align="center">
<p>
需要安装帮助？有问题或奇思妙想？ 💡 想观看实时演示、测试专属微调模型，或直接与人格引擎驱动的角色聊天？在RVC模型转换、自定义Live2D模型绑定遇到问题？快来Discord找我们！ 👋
</p>
<a href="https://discord.gg/p3CXEyFtrA" target="_blank">
<img src="assets/discord.png" alt="加入Discord"
  width="400"
  /></a>
  <br>
<a href="https://discord.gg/p3CXEyFtrA" target="_blank">
<img src="https://img.shields.io/discord/1347649495646601419?label=加入Discord&logo=discord&style=for-the-badge" alt="加入Discord徽章" />
</a>
<br>
<br>
<p>你也可以通过 <a href="https://github.com/fagenorn/handcrafted-persona-engine/issues" target="_blank">GitHub Issues</a> 提交Bug反馈或功能需求。</p>
</div>

## <a id="support"></a>❓ 支持与联系

* **主要支持渠道 & 社区：** 加入我们的 [Discord服务器](#community) 获取帮助、参与讨论和观看演示。
* **Bug反馈 & 功能需求：** 通过 [GitHub Issues](https://github.com/fagenorn/handcrafted-persona-engine/issues) 提交。
* **直接联系：** 也可通过 [Twitter/X](https://x.com/fagenorn) 联系我们。

-----

> [!TIP]
> *自定义虚拟形象开发请参考 [Live2D 集成与绑定指南](./Live2D.md)。*
> *详细安装配置步骤请查阅 [安装与配置指南](./INSTALLATION.md)。*
