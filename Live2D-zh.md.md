<div align="center">
<h1>
🎭 Live2D 模型集成与绑定指南 🎭
</h1>
<img src="assets/mascot_wand.png" width="150" alt="手持魔杖的吉祥物">
<p>让你的 Live2D 虚拟形象适配 Persona Engine 吧！</p>
</div>

## 1. 概述：内容总览 🌸

本文档详细说明 Persona Engine 中 Live2D 动画系统的功能，并为制作兼容该系统的 Live2D 模型的绑定师和设计师提供核心规范。这份指南就像赋予角色数字灵魂的蓝图！✨

该系统由多个 C# 服务协同运作，如同精密的机器：

1.  **`EmotionAnimationService`（情感动画服务）**：处理由情感线索触发的表情和全身动作，这些线索通常来自 AI 人格（如 Aria），基于检测到的表情符号 😊。
2.  **`IdleBlinkingAnimationService`（闲置眨眼动画服务）**：管理默认的闲置动画和自然的自动眨眼效果 👀。
3.  **`VBridgerLipSyncService`（唇形同步服务）**：利用带时间戳的音素数据，严格遵循 **VBridger 参数标准**，让模型的嘴部动作 👄 与语音同步。
4.  **大语言模型（LLM）集成**：AI 模型（如为「Aria」定义的模型）生成包含特定情感标签（例如 `[EMOTION:🤩]`）的文本回复，这些标签会被解析并交由 `EmotionAnimationService` 处理。

严格按照下文规范进行绑定，是确保模型按预期运行、充分发挥系统功能的**关键**。接下来让我们深入了解！

## 2. 情感系统（`EmotionAnimationService`）❤️‍🔥

这个服务让角色的情感直观呈现！

### 功能说明

* **触发机制**：情感主要由控制型 AI（如 Aria）生成的文本中嵌入的特定表情符号标签（例如 `😊`、`😤`、`🤩`）触发。系统会检测这些标签，并映射到对应的 Live2D 动作。
* **映射规则**：服务内的 `EmotionMap` 字典定义了每个识别到的表情符号对应的 Live2D 表情和/或动作组。
    * 示例：`{ "😊", new EmotionMapping("happy", "Happy") }` 表示将 😊 表情符号映射到名为 "happy" 的表情，以及从名为 "Happy" 的动作组中随机选取一个动作。
* **表情控制**：当触发带有映射表情的情感时，该表情会应用到模型上。
    * 表情会保持设定时长（`EXPRESSION_HOLD_DURATION_SECONDS`，默认值：3 秒）。
    * 时长结束后，或播放停止且无新情感覆盖时，模型会尝试恢复到预设的中性表情（`NEUTRAL_EXPRESSION_ID`，默认值："neutral"）。
* **动作控制**：如果某一情感映射到某个动作组，系统会从该组中随机选取一个动作，并以高优先级（`EMOTION_MOTION_PRIORITY`，默认值：`PriorityForce`）播放。这使得情感动作能够覆盖闲置或中性对话动画。
* **中性对话**：在语音播放过程中，若未激活特定情感动作，系统会从指定的中性对话组（`NEUTRAL_TALKING_MOTION_GROUP`，默认值："Talking"）中随机播放动作，优先级为普通（`NEUTRAL_TALKING_MOTION_PRIORITY`，默认值：`PriorityNormal`）。

### 表情符号 -> 表情/动作映射表

以下是默认表情符号与 Live2D 资源的映射关系。**你的表情和动作组名称必须与表中完全一致！**

| 表情符号 | `ExpressionId`（必填名称） | `MotionGroup`（必填名称） | 描述 / 预期视觉效果                                                                 |
| :------- | :------------------------- | :------------------------ | :---------------------------------------------------------------------------------- |
| 😊       | `happy`                    | `Happy`                   | 通用开心表情，笑容开朗，眼神明亮。动作：积极、轻柔的肢体动作。                        |
| 🤩       | `excited_star`             | `Excited`                 | 星星眼，笑容灿烂，活力满满。动作：活泼、夸张，可包含拍手等动作。                      |
| 😎       | `cool`                     | `Confident`               | 略带得意的笑，可添加墨镜效果（若已绑定）。动作：流畅、自信的姿势/肢体动作。            |
| 😏       | `smug`                     | `Confident`               | 坏笑，半睁的眼睛，了然的神情。动作：与 cool/confident 类似，可添加歪头动作。           |
| 💪       | `determined`               | `Confident`               | 眼神专注，下颌微紧（幅度要小！），站姿自信。动作：有力的姿势，可包含握拳鼓劲动作。    |
| 😳       | `embarrassed`              | `Nervous`                 | 满脸通红，眼神躲闪，可能略带皱眉。动作：坐立不安，身体微微蜷缩。                      |
| 😲       | `shocked`                  | `Surprised`               | 眼睛睁大，嘴巴微张（幅度适中，避免与唇形同步冲突！），眉毛上扬。动作：后退、惊跳。    |
| 🤔       | `thinking`                 | `Thinking`                | 眉头微皱，视线看向侧面/上方，可能手托下巴。动作：歪头、轻摸下巴。                      |
| 👀       | `suspicious`               | `Thinking`                | 眼睛眯起，略带斜视，表情中性/微皱眉。动作：身体微微前倾。                              |
| 😤       | `frustrated`               | `Angry`                   | 脸颊鼓起（幅度要小！），眉头紧锁，可添加蒸汽/压力特效（若已绑定）。动作：跺脚、幅度大的肢体动作。 |
| 😢       | `sad`                      | `Sad`                     | 嘴角下撇，眼神含泪/悲伤，眉毛低垂。动作：垂头丧气，身体瘫软。                          |
| 😅       | `awkward`                  | `Nervous`                 | 流汗特效（若已绑定），尴尬的笑容，眼神躲闪。动作：坐立不安，挠头。                      |
| 🙄       | `dismissive`               | `Annoyed`                 | 翻白眼（需做动画！），略带皱眉或不屑的表情。动作：转头、叹气。                          |
| 💕       | `adoring`                  | `Happy`                   | 爱心眼特效（若已绑定），笑容温柔，脸颊泛红。动作：身体前倾，轻轻摇晃。                  |
| 😂       | `laughing`                 | `Happy`                   | 眼睛紧闭，笑容夸张（注意避免与唇形同步冲突！），可能带泪。动作：身体抖动，捧腹。        |
| 🔥       | `passionate`               | `Excited`                 | 火焰眼特效（若已绑定），神情坚定/亢奋。动作：活力十足，幅度大的肢体动作。              |
| ✨       | `sparkle`                  | `Happy`                   | 闪光眼特效（若已绑定），表情明亮开心。动作：轻柔、积极的肢体动作，可添加旋转动作。    |
| *无*     | `neutral`                  | *无* | 角色默认的放松表情。                                                                 |
| *无*     | *无* | `Talking`                 | *无* - 用于中性对话时的轻微背景动作。                                                 |

### 绑定指南

* **表情制作**：
    * 创建与表中 `ExpressionId` 名称**完全一致**的独立表情。
    * **❗ 关键要求**：必须创建与 `NEUTRAL_EXPRESSION_ID`（默认值：`neutral`）完全同名的中性表情。缺少该表情会导致模型无法正常恢复默认状态！
    * **❗ 唇形同步优先级**：表情应主要作用于**眼睛、眉毛、腮红及其他非嘴部面部特征**。避免大幅修改核心唇形同步参数（如 `ParamMouthOpenY`、`ParamJawOpen`、`ParamMouthForm`、`ParamMouthPuckerWiden`、`ParamMouthPressLipOpen`），这些参数在语音播放时会由 `VBridgerLipSyncService` 主动控制。表情设计需**配合**语音，而非覆盖嘴部形态。
* **动作组制作**：
    * 创建与表中 `MotionGroup` 名称**完全一致**的动作组（区分大小写）。
    * 在组内添加 `.motion3.json` 文件，对应合适的动画效果。
    * **❗ 聚焦身体/头部**：动作应主要围绕**身体动作、头部倾斜/点头/摇头、手臂姿势、整体体态变化**设计。虽然动作中可包含面部参数调整，但需注意：嘴部参数可能会被唇形同步覆盖，眼睛/眉毛参数可能会被激活的表情覆盖。动作设计需适配对话和情感表达场景。
    * **❗ 中性对话动作**：需创建专门的中性对话动作组（包含轻微点头、重心小幅转移等动作），名称必须与 `NEUTRAL_TALKING_MOTION_GROUP`（默认值：`Talking`）完全一致。这是保证模型在中性对话时生动的关键！
* **优先级设置**：注意动作优先级规则（情感动作为 `PriorityForce`，中性对话动作为 `PriorityNormal`）。确保闲置动画（见下一节）使用更低优先级（`PriorityIdle`）。
* **过渡效果**：为实现表情/动作间的平滑切换，需在 Live2D 编辑器中为 `.exp3.json` 或 `.motion3.json` 文件设置 `FadeInTime`（淡入时间）和 `FadeOutTime`（淡出时间）。详见 [第 6 节](#最佳实践)。

## 3. 闲置与眨眼系统（`IdleBlinkingAnimationService`）😴

即使在无交互状态下，也能让角色保持生动。

### 功能说明

* **闲置动画**：当无更高优先级动作激活时，该服务会从指定的「Idle」组（`IDLE_MOTION_GROUP`，默认值："Idle"）中随机播放动作，优先级为低（`IDLE_MOTION_PRIORITY`，默认值：`PriorityIdle`）。
* **自动眨眼**：该服务直接控制睁眼参数（`ParamEyeLOpen`、`ParamEyeROpen`），模拟随机间隔的自然眨眼效果（间隔范围：`BLINK_INTERVAL_MIN_SECONDS` 至 `BLINK_INTERVAL_MAX_SECONDS`）。眨眼过程遵循固定的时间规律（闭眼、闭合、睁眼时长）。除非表情强制设定眼睛闭合/睁开，否则眨眼会自动触发。

### 绑定指南

* **闲置动作组**：
    * 创建与 `IDLE_MOTION_GROUP`（默认值：`Idle`）完全同名的动作组。
    * 组内添加轻微的循环动画（呼吸、小幅摇晃、体态微调等）。
    * 确保这些动作的优先级为 `PriorityIdle`。
* **眼睛参数**：
    * ✅ **关键要求**：模型必须使用 Live2D 标准眼睛参数：`ParamEyeLOpen`（左眼睁开度）和 `ParamEyeROpen`（右眼睁开度）。
    * 这些参数需控制眼睛垂直开合程度，取值范围为 `0.0`（完全闭合）至 `1.0`（完全睁开）。
    * 绑定这些参数时，需确保闭眼/睁眼动画过渡流畅。
    * `BLINK_CLOSING_DURATION` 等常量定义了眨眼速度——绑定参数时需保证动画过渡流畅，适配该速度。

## 4. 唇形同步系统（`VBridgerLipSyncService`）👄

实现逼真语音动画的核心模块！

### 功能说明

* **❗ 标准要求**：该服务**仅适配遵循 VBridger 参数标准绑定的模型**。若模型仅使用基础的 `ParamMouthOpenY` 或其他唇形同步规范，将无法正常工作。
* **输入数据**：依赖 `TimedPhoneme` 数据（来自 TTS 语音分析），包含音素（/a/、/i/、/s/ 等）及其时间戳。
* **映射规则**：详细的 `_phonemeMap` 字典将音素转换为目标 `PhonemePose` 结构体，定义该嘴型对应的多个 VBridger 参数目标值。
* **插值与平滑**：基于音频时间，通过 `Lerp`（线性插值）和平滑因子实现音素姿势间的平滑过渡，让嘴部动作更自然。
* **受控参数**：直接操控一组特定的 VBridger 参数。

### 绑定指南

* **!!! 核心要求：遵循 VBridger 标准 !!!**
    * 模型**必须**按照标准 VBridger 参数集进行绑定。如需参考，可查阅 VBridger 官方文档和教程。
    * 该服务会**显式控制**以下参数，需确保参数存在且绑定正确：
        * `ParamMouthOpenY`：嘴部垂直开合度。
        * `ParamJawOpen`：下颌开合度。
        * `ParamMouthForm`：嘴角形态（-1 撇嘴 至 +1 微笑）。
        * `ParamMouthShrug`：嘴唇向上紧绷度。
        * `ParamMouthFunnel`：嘴唇噘起/收拢程度（对应「呜」音）。
        * `ParamMouthPuckerWiden`：嘴部水平形态（-1 张大 至 +1 噘起）。
        * `ParamMouthPressLipOpen`：嘴唇分离度（-1 抿紧 至 0 贴合 至 +1 分开/露齿）。
        * `ParamMouthX`：嘴部水平偏移（-1 左偏 至 +1 右偏）。
        * `ParamCheekPuffC`：脸颊鼓起程度（0 至 1）。
* **参考姿势**：代码中的 `InitializeMisakiPhonemeMap_Revised` 函数可作为参数目标形态的参考。例如，音素 "i"（对应「伊」音）的参数配置：
    ```csharp
    // map.Add("i", new PhonemePose(openY: 0.1f, jawOpen: 0.1f, form: 0.7f, shrug: 0.4f, puckerWiden: -0.9f, pressLip: 0.9f));
    // 绑定要求：这些参数值需呈现出「伊」的视觉形态——嘴微张、嘴角上扬明显、嘴唇轻微上提、嘴部大幅张开、露出牙齿。
