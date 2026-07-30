#简历 

> 本文整合《〈鸣潮〉Event 事件系统深度拆解》与《鸣潮 VO 语音命名系统完整总结》两份分析，将 **Event 全集（24,042 个事件）** 与 **VO 语音命名空间（6,756 个事件）** 放进同一个框架：事件系统是母体，语音系统是其中一个按同一命名哲学运转的子系统；两者共用一套"上下文 Token 堆叠"命名语言。

---

# 第一部分　总体定位：两套数据、一个系统

## 1.1 两个分析对象

| 命名空间 | 文件数 | 显式事件名 | 主体操作 | 占比 |
|---|---:|---:|---|---:|
| `Event/`（全集） | 24,042 | 17,203 | `play`（21,276） | play 约 88.5% |
| `VO/`（语音子空间） | 6,756 | 6,744 | `play`（6,724） | play 约 99.5% |

VO 不是独立于 Event 的另一套系统，而是**同一命名空间中以语音内容为主的投射面**：

- Event 全集里明确归 `vo` 的路由有 724 个事件（`play/vo`），但语音实际还分散在 `play_mon_..._vo`、`play_boss_..._death_vo`、`play_favor_word_...`、`play_plot_...`、本地化包装层等多个分支；
- VO 目录本身（6,756 文件）就是把这些语音相关事件按前缀树重新聚合后的视图。

## 1.2 系统的最终定义

> **《鸣潮》Event 系统是一个介于游戏逻辑与 Wwise 之间的、规模庞大的音频业务接口层。它把"游戏中发生了什么"转换为"音频系统应该如何响应"。**

> **VO 子系统是其中负责语音呈现的部分：它也不是录音素材库，而是角色系统、怪物动画、任务剧情、UI、空间音频和技术混音等多条生产管线共同投射到一个事件命名空间后的结果。**

合并两份文档的总公式：

```text
《鸣潮》Event 系统
=
命令命名空间
+ 游戏业务本体
+ 内容包归属
+ 动作同步点注册表
+ 状态与生命周期 API
+ 语音呈现系统（VO）
+ 音频生产历史
```

## 1.3 运行链路

```text
游戏逻辑
│
├── AI状态机
├── Gameplay Ability
├── Animation / Montage
├── Sequencer
├── 地图系统
├── UI系统
├── 剧情任务系统
└── 语音呈现系统
        ↓
语义化 Event 名称或 Short ID
        ↓
UAkAudioEvent / PostAkEvent
        ↓
AK::SoundEngine::PostEvent
        ↓
CAkEvent → Action List → 目标 HIRC 对象
        ↓
Sound / Container / Music / Bus / State
        ↓
SoundBank 与媒体文件
```

目录树能直接证明的是上半部分的**语义化 Event 接口**；从 `CAkEvent → Action → HIRC Target` 开始属于结合 Wwise 原理的系统解释，不能仅凭事件名断定 Event 内部包含几条 Action。

## 1.4 树的本质：前缀树（Trie），不是真实文件夹

两份分析共同确认：目录是**由 Event 名称按下划线切分后生成的前缀树**，不是 Wwise 工程结构。

证据链：

- Event 全集：17,199 个显式事件的目录路径都能与事件名下划线前缀一一对应；
- VO 子集：4,537 个 JSON 名完全等于路径扁平化，2,207 个等于路径扁平化加末尾变体，**0 个发生中间字段重排**；
- 唯一例外是 `files` 组织节点（如 `play/boss/qunnie/bat/files/` 下的事件叫 `play_boss_qunnie_bat_vo_01`，名中无 `files`）。

因此目录树反映的是**事件命名空间**，不是 Actor-Mixer Hierarchy、Content Browser 或 SoundBank 物理目录。

由此得到一个统一的命名公式：

```text
EventName = Join(PathTokens, "_") + OptionalLeafSuffix
```

并且必须区分三层对象：

```text
事件组目录（公共前缀）
≠ JSON 事件（可调用的独立接口）
≠ 事件内部最终播放的音频文件
```

---

# 第二部分　统一命名理论：上下文 Token 堆叠

## 2.1 命名不是固定列，而是逐渐补充上下文的句子

两份文档的核心共识：鸣潮事件名**不是数据库式的固定字段结构**（"第1段永远是操作、第2段永远是角色"不成立），而是每加入一个 Token 就进一步缩小运行时上下文。

合并后的完整抽象形式：

```text
<operation>
_<route_owner>
_<content_scope?>
_<entity_class?>
_<entity_id?>
_<form?>
_<domain?>
_<action_or_node?>
_<phase?>
_<presentation?>
_<audio_layer?>
_<variant?>
_<media_marker?>
```

问号表示该字段并非所有事件都有。程序化统计显示：显式 Event 名最少 2 个 Token，最多 11 个，中位数约 5 个——它是**可变长度的语义串**。

## 2.2 同一事件名的多分支语法

不同分支采用不同命名语法，不能用一套固定字段位置解析全部事件：

```text
play/vo/anke/atk01            → 操作 / VO路由 / 角色 / 动作
play/boss/feilian/bat/atk03   → 操作 / 敌人等级 / 实体 / 战斗域 / 动作
play/vo/main/linaxita/2_10_51_nosub → 操作 / VO路由 / 内容线 / 地区篇章 / 剧情节点
play/mon/azizi/attack01       → 操作 / 怪物系统 / 实体 / 动作
```

统一性不在"每段位置永远相同"，而在"每个 Token 都在收窄上下文"。

## 2.3 Token 分类总表（合并版）

分析这棵树时必须区分以下类别，不能机械地把目录名当业务字段：

| 类别 | 例子 |
|---|---|
| 操作字段 | `play`、`stop`、`set`、`pause`、`mute` |
| 生命周期字段 | `enter`、`exit`、`reset`、`start`、`loop`、`end` |
| 稳定业务字段 | `role`、`mon`、`boss`、`map`、`vo` |
| 动作字段 | `attack`、`born`、`death`、`patroltofight` |
| 声音职责字段 | `foley`、`vo`、`hit`、`whoosh`、`imp`、`fx` |
| 呈现/空间字段 | `nosub`、`amb`、`2d`、`3d`、`3d_far` |
| 状态字段 | `stage1`、`danger`、`safe`、`silence`、`none` |
| 偶然语法词 | `the`、`no`、`to`、`view` |
| 内部生产代码 | `M2`、`R01003`、`LVB` |
| 历史拼写错误 | `plau`、`commmon`、`stete`、`paralysisl`、`transofrm` |

---

# 第三部分　第一层：Operation 操作命令

## 3.1 操作全集（Event 全集视角）

根节点混合三种语义：

**① 操作命令**

```text
Play  Stop  Set  Pause  Mute  Unmute  Enable  Disable  Open  Finish  Clean  Clear
```

**② 生命周期命令**

```text
Enter  Exit  Reset  Finish  OnWorldCleanup  OnWorldDone
```

**③ 业务所有者（直接以系统名开头、无显式操作）**

```text
Map  Sequence  Role  Mon  Plot  UI  Story
```

所以根节点不是统一的"声音分类"，而是：

```text
命令 + 系统入口 + 历史生产路径
```

## 3.2 顶层分支规模（Event 全集）

| 顶层分支 | 事件数 | 约占全部 |
|---|--:|--:|
| `play` | 21,276 | 88.50% |
| `sfx` | 819 | 3.41% |
| `set` | 501 | 2.08% |
| `sequence` | 369 | 1.53% |
| `stop` | 260 | 1.08% |
| `map` | 227 | 0.94% |
| `mon` | 144 | 0.60% |
| `enter` | 99 | 0.41% |
| `role` | 85 | 0.35% |
| `plot` | 65 | 0.27% |
| `ui` | 62 | 0.26% |

## 3.3 四大主操作详解

### `play`：启动声音事件

占绝对主体。VO 子集中 99.53% 的文件都在 `play` 分支。

### `stop`：终止需要显式管理生命周期的声音

```text
stop_vo_main_linaxita_2_10_51_nosub_01_amb
stop_vo_mon_wumingtansuozhe_breath_loop_heavy
```

关键事实（VO 子集）：**全部 10 个 stop 事件都能找到同名内容键对应的 play 事件**。名称本身包含可计算关系：

```text
content_key = remove_prefix(play_) = remove_prefix(stop_)
```

这种设计方便自动寻找配对、检查缺失 Stop、管理场景退出、防止声音泄漏。

### `set`：改变声音呈现或混音状态

基本公式：

```text
set_<context>_<target>_<desired_state>
```

```text
set_gacha_music_volume_silence
set_scene_music_yrsj_night_no_vocal
set_volume_down_amb_3d_task_tiancheng_zhong
```

其中 `set_state_*` 已表现出明显的枚举结构（见第八部分 State 系统）。

### `enter` 与无显式操作的 `mon`

```text
enter_wild_cxs_no_vo        # 进入某种野外/语音上下文（证据不足，仅少量事件）
mon_gulong_bat_vo_attack_death   # 无 play 前缀的怪物直连事件
```

`mon_*` 直连事件证明项目中存在**标准操作前缀体系 + 历史直连体系**两代结构共存。

---

# 第四部分　第二层：Route Owner 业务路由

## 4.1 核心原则

> **Event 主要按"谁调用、在哪种业务上下文使用"组织，而不是按"它听起来是什么声音"组织。**

`play` 后面的第二段不是固定的"声音类型"，而是混合了：对象等级（`boss`、`elite`、`lord`、`ord`）、对象类型（`mon`、`npc`、`role`）、游戏功能（`favor`、`task`、`ui`、`vision`）、上游系统（`sequence`、`interact`）、媒体类型（`music`、`bgm`、`sfx`、`foley`）、特定角色、语言覆盖（`zh`）。

## 4.2 `play` 的业务域全景（Event 全集）

| `play` 子域 | 数量 | 主要意义 |
|---|--:|---|
| `mon` | 2,936 | 普通怪物与敌人 |
| `role` | 2,676 | 可操作角色和角色系统 |
| `sfx` | 2,308 | 通用、临时及技术接入音效 |
| `ui` | 1,670 | 界面、功能和活动 |
| `boss` | 1,567 | Boss 战斗包 |
| `interact` | 1,439 | 场景交互与关卡对象 |
| `story` | 1,280 | 主要是剧情音乐 |
| `amb` | 1,246 | 环境部署与环境对象 |
| `vo` | 724 | 明确归入 VO 的语音 |
| `plot` | 634 | 剧情演出综合声音包 |
| `ost` | 312 | 原声及专辑内容 |
| `vision` | 262 | 视觉、幻象或相关效果 |
| `task` | 260 | 任务内容包 |
| `elite` | 254 | 精英敌人 |
| `foley` | 240 | 角色与对象动作声音 |
| `favor` | 238 | 角色好感、档案等内容 |
| `music` | 206 | 通用音乐调用 |

## 4.3 VO 子集的三大主干

VO 命名空间中三个最大分支合计占 `play` 的约 93.78%：

```text
play/vo      5249    通用 VO 内容
play/mon      581    怪物动作发声
play/favor    476    角色语音变体／档案试听
```

这说明语音系统的核心不是 `set` 或 `stop`，而是三种播放模式：**通用 VO 内容、怪物动作发声、角色语音变体/档案试听**，其余任务、UI、演出、混音功能围绕它们扩展。

## 4.4 关键修正：`play/story` 不是剧情对白

`play/story` 共 1,280 个事件，其中 Music 1,272 个、Quest 8 个——**约 99.4% 是剧情音乐**。真正的语音内容分散在 `play/vo`、`play/favor/word`、角色和怪物行为内部的 `_vo`、`plot`、`task`、`external` 与本地化包装层。

这再次证明：Event 系统是**调用上下文本体**，不是媒体类型本体。同一种 VO 可能出现在：

```text
Play_VO_...
Play_Mon_<Monster>_Attack_VO
Play_Boss_<Boss>_Death_VO
Play_Favor_Word_...
Play_Plot_...
```

## 4.5 VO 子集的主要路由

| 路由 | 含义 | 示例 |
|---|---|---|
| `play_vo` | 通用 VO 系统拥有的内容（大型内容路由） | `play_vo_anke_atk01` |
| `play_mon` | 怪物／AI／动画系统拥有的声音事件 | `play_mon_azizi_attack01_vo` |
| `play_favor_vo` | 角色好感/语音档案系统的直接变体接口 | `play_favor_vo_jianxin_atk01_01` |
| `play_task` | 任务逻辑直接触发 | `play_task_laliao_approval_vo` |
| `play_ui` | UI 操作和状态反馈 | `play_ui_fishing_octopus_vo_buy` |
| `play_sequence` | 过场或 Sequence 系统的音频触发 | `play_sequence_music_sfx_vo_a01003` |
| `play_external` | 字幕与 Ducking 策略接口 | `play_external_vo_bubble_soft_ducking` |

---

# 第五部分　内容域分系统拆解

## 5.1 角色语音系统：三代命名演化

角色命名是整套系统中演化最明显的部分。

### 第一代：平铺式角色包

```text
play_vo_anke_atk01
play_vo_anke_behit
play_vo_anke_fast_run
play_vo_anke_hp30
play_vo_anke_join_team
```

公式：`play_vo_<character>_<event>`。问题是战斗、探索、受击、角色资料、好感、养成、系统反馈全部混在同一层。

### 第二代：功能域模板

新角色开始使用功能域：

| 域 | 含义 | 典型槽位 |
|---|---|---|
| `com` | 公共角色行为接口 | `accelerate`、`behit`、`die`、`engage`、`jump`、`limitdodge`、`openbox`、`hpdown01～03`、`parry`、`tired` |
| `atk` | 普攻、重击、下落攻击、闪避攻击 | `atk_atk01`、`atk_heavyatk01`、`atk_fallingatk_start`、`atk_dodgeatk` |
| `burst` | 共鸣解放/爆发技能 | `burst_burst01`、`burst_burst01_start`、`burst_burst01_end` |
| `skill` | 技能、QTE、形态切换、专属机制 | `skill_skill01`、`skill_qte`、`skill_formchange`、`skill_exitskill` |
| `idle` | 待机演出 | `idle_idle01`、`idle_standchange` |
| `sys` | 角色系统和养成 | `sys_gacha`、`sys_jointeam`、`sys_birthcele`、`sys_rankup01` |

`atk_atk01` 表面像重复，实际是两级结构：**第一段是功能域，第二段是域内动作槽位**：

```json
{
  "operation": "play",
  "route": "vo",
  "character": "katixiya",
  "domain": "atk",
  "slot": "atk01"
}
```

### 第三代：形态和机制扩展

多形态角色在角色名和功能域之间插入形态：

```text
play_vo_aimisi_humanform_atk_atk01
play_vo_aimisi_mechaform_skill_boost_start
```

最终公式：

```text
play_vo_<character>_<form?>_<domain>_<action>_<phase?>_<variant?>
```

### 演化的本质：从"描述表现"到"Gameplay 接口槽位"

| 旧命名 | 新命名 |
|---|---|
| `fast_run` | `com_accelerate` |
| `enter_battle` | `com_engage` |
| `chest` | `com_openbox` |
| `hp70` / `hp50` / `hp30` | `com_hpdown01` / `02` / `03` |
| `evasion_success` | `com_limitdodge` |

`hp30` 把 30% 阈值写死在事件名里；`hpdown03` 只表示第三档低血量事件，策划改触发值为 25% 或 35% 时音频事件名不用变。新模板更适合：自动生成事件、数据表驱动、Gameplay Tag、Ability System、动画通知、缺失槽位自动检查、多语言资源同步、新角色复用模板。

## 5.2 `favor` 的真正作用：录音变体直接访问层

`favor` 下只有四个角色（`jianxin`、`lingyang`、`qiushui`、`taoqi`），内容几乎复制标准角色包，但战斗、移动、受击等事件从一个事件扩展成多个编号事件：

```text
标准运行时：  play_vo_jianxin_atk01            （运行时包装事件，内部自选变体）
favor 分支：  play_favor_vo_jianxin_atk01_01
              play_favor_vo_jianxin_atk01_02
              play_favor_vo_jianxin_atk01_03   （逐条试听事件）
```

高置信度解释：`favor` 是**由好感或角色语音档案界面拥有的"录音变体直接访问层"**，让用户在角色资料页单独试听每一条战斗语音。名称中没有明确的 `favor_level` 字段，因此"好感等级切换语音"的解释证据不足。

## 5.3 怪物语音：两套平行系统

| 路径 | 事件所有者 | 示例 |
|---|---|---|
| `play_mon` | 怪物 AI、动画或怪物系统 | `play_mon_azizi_attack01_vo`、`play_mon_azizi_patroltofight_vo` |
| `play_vo_mon` | 通用 VO 内容系统（显式列出字母变体） | `play_vo_mon_bingjuedoushi_atk07_a` ～ `_e` |

不能简单理解为 `play_mon` = 动物叫声、`play_vo_mon` = 会说人话——机械、人形和特殊敌人都可能出现在两种体系中。

### 怪物行为状态机

怪物事件反复出现的动作可抽象为一条状态链：

```text
Born 生成
  ↓
Stand / Patrol 待机 / 巡逻
  ↓
PatrolToFight 发现目标
  ↓
Attack / Skill 战斗
  ↓
BeHit / Block / Fly 受击
  ↓
StandUp 恢复
  ↓
Death / DeathInWater 死亡
```

正确关系是：**AI 决定"发生了什么"，Event 决定"通知音频系统发生了什么"，Wwise 决定"具体播放哪些声音对象"**。Wwise 并不运行怪物 AI。

### 怪物事件是动画资产名称的镜像

怪物语音依附于已存在的动作资产：

```text
动画 / Montage / Ability
      ↓
Animation Notify 或行为节点
      ↓
调用同名 VO Event
      ↓
Wwise 播放声音
```

证据：命名中出现 `at_frame_1730`、`montage`、`atk04_start`、`atk06_weak_end`、`inplacehit` 等动画管线痕迹；也因此继承了上游的历史差异与拼写错误（`atk/attack`、`deathinwater/death_inwater`、`paralysisl`、`transofrm`、`aattack`）。

### Boss / Elite / Lord / Ord 不是绝对实体属性

同一实体可能出现在不同路径（`play/boss/huiying` 与 `play/lord/huiying`；`play/mon/binglie` 与 `play/ord/binglie`）。这些词表示的是**当前玩法等级、战斗模板或调用路由**，不是实体数据库中的永久生物分类。数据库中应保存：

```json
{
  "entity": "huiying",
  "event_route_classifications": ["boss", "lord"],
  "canonical_entity_class": null
}
```

### Boss 包的特殊性

`play/boss` 有 1,567 个事件、集中在 17 个 Boss 包（`qishi` 184、`fuludelisi` 179、`shanghen` 162、`rongyaoshixiang` 133、`qunnie` 126……）。特点：攻击拆得极细、包含阶段切换/瘫痪/受击/死亡、可能包含玩家角色或演出对象、常与 Montage/Sequence/剧情战绑定。

因此 `Play_Boss_Fuludelisi_...` 不一定表示"发声者是芙露德莉斯"，而表示"该事件属于芙露德莉斯 Boss 战内容包"。必须区分：

```text
package_owner ≠ source_entity ≠ target_entity ≠ related_entity ≠ encounter_context
```

## 5.4 通用 NPC：声音原型池

NPC 目录采用"年龄与性别声线原型 × 声音套装 × 台词编号"的三层模型：

```text
play_vo_npc_<voice_archetype>_<voice_set>_<line_index>

原型：childboy / childgirl / teenboy / teengirl / male / female / oldmale / oldfemale
套装：a / b / c
示例：play_vo_npc_childboy_a_01 ～ _24
```

A、B 通常各有 21～24 条完整平行序列，很可能代表两名配音演员或两套声线；C 通常只有 1～3 条，更可能是后续补录或尚未完整建立的第三声线包。

## 5.5 剧情语音：内容包 + 节点组织

```text
play/vo/main/{lahairoi, linaxita, rinascita, ryam, ygdx, yhx}/2_10_50_nosub/
→ play_vo_main_linaxita_2_10_50_nosub_01
→ play_vo_main_linaxita_2_10_50_nosub_01_amb   （环境版）
```

拆解：`play` 操作 / `vo` 路由 / `main` 主线 / `linaxita` 地区篇章 / `2_10_50` 节点标识 / `nosub` 无普通字幕 / `01` 节点内实例 / `amb` 环境式播放版本。

**剧情编号不能机械拆解**：同一地区下既有 `3_1_35_nosub`，也有 `byhm_37_nosub`、`wmxztk_56_nosub`——中间部分可能混合版本、任务代码、内容包代码、剧情节点、行号、演出节点。不要把 `2_10_51` 武断拆成"第二章/第十任务/第51句"。

## 5.6 地图系统：最稳定的生命周期 API

```text
Map_<MapType>_<MapID>           初始化默认音频配置
Map_<MapType>_<MapID>_Enter     进入该地图
Map_<MapType>_<MapID>_Exit      离开并退出相关状态
Map_<MapType>_<MapID>_Reset     清除临时状态、恢复默认值
```

用于防止：上一张地图音乐状态残留、环境层未停止、临时混音状态泄漏、Boss 状态进入普通世界、剧情静音未清除。

`MusicReset_Deprecated` 系列事件揭示了管线重构痕迹：旧方案 Map Reset 与 Music Reset 分别调用，新方案统一由 Map Reset 或新的 Music/State 系统恢复——这是在线游戏长期维护和接口迁移的直接证据。

## 5.7 State 系统：状态组与状态值

```text
Set_State_Gongduola_On / _Off
Set_State_Dungeon_Zanni_Danger / _Safe
Set_State_Heixiazi_Aoxiang_0 / _1 / _2
```

可抽象为 `SetState("Group", "Value")`。状态值包括：`Calm`、`Sadness`、`Silence`、`Funny`、`Warm`、`Night`、`Explore`、`Drown`、`Boss`、`None`、`Stage1～3`。状态系统不仅服务战斗，还控制音乐情绪、剧情氛围、夜晚环境、Boss 阶段、地图危险程度、角色演出、静音、任务阶段、混音和音乐层。

注意：目录只能证明 Event 名表达"设置状态"，不能证明内部一定直接调用 Wwise `SetState()`——也可能是一个 Event 内部包含 Set State Action。

## 5.8 音乐系统：叙事状态机，不是播放曲目

剧情音乐按多维度组织：版本（`1_3`～`3_4`）、角色或故事包（`Anke`、`Aogusita`、`Katixiya`……）、剧情/任务编号（`M2`、`M01003`、`7_01`）、叙事功能或情绪（`Calmness`、`Dangerous`、`Horror`、`Suspense`、`Sadness`、`Warm`、`Silence`）。

剧情系统请求的不是"播放某一首音乐文件"，而是：

```text
进入某个剧情 Cue / 设置某个音乐状态 / 进入某个情绪 / 切换某个段落 / 触发某个 Stinger
```

音乐体系 ≈ **叙事 Cue + State + Layer + Stinger + 生命周期**。

## 5.9 环境声系统：按部署方式组织

| 类型 | 含义 | 示例 |
|---|---|---|
| `Bed` | 大范围连续环境底 | `Amb_Bed_RoomTone_Medical_Room_Loop`（风、房间底噪、城市底） |
| `Emit` | 挂在 3D 对象上的局部声源 | `Amb_Emit_Machine_Computer_Home`（机器、火焰、屏幕、植物） |
| `NPC` | 环境生物、群众的行为声 | `Amb_NPC_Alien_Wutata_Shake_Head` |
| `Interact` | 交互对象的持续或状态声音 | — |
| `Weather` | 雨雪等全局或区域天气层 | `Amb_Weather_Rain_Reverse` |

环境系统回答的是"声音怎样被部署到世界中"，而不只是"属于哪张地图"。

## 5.10 交互系统：关卡设计与技术音频的交界

`play/interact` 有 1,439 个事件，内容来自 `Seq`、`Level`、`TPrefab`、`Space`、`Printer`、`Cyberpunk`、`Fishing`、`Cube`、`Search`、`Task` 等——它不是单纯的"按 E 键物件音效"，而是关卡设计、场景资产、Prefab、Sequence、机关、谜题、任务、活动玩法、技术演出的**跨部门接入区**，也是最容易积累临时命名和项目债务的分支之一。

## 5.11 Sequence 与 `LevelB`

```text
Sequence_LevelB_Main_<M编号>_<Cue>     sequence_levelb_main_m01002_1z / _2a / _4c
Sequence_LevelB_Role_<Character>_<R编号>_<Cue>
```

| 字段 | 可能意义 |
|---|---|
| `Main` / `Role` | 主线内容 / 角色剧情 |
| `Mxxxxx` / `Rxxxxx` | 主线、任务或演出 ID / 角色剧情或演出 ID |
| `1Z / 2A / 4C` | 镜头段、Cue 段或声音触发点 |
| `LevelB` | 很可能与 Level Blueprint 或关卡级演出接入层相关（高置信度推断，正式全称未知） |

## 5.12 角色 UI：高度标准化的接口

多个角色反复使用同一模块结构：

```text
UI/{Chip, Nature, Resonant, Weapon}/{Start, Loop, End}

Play_Augusta_UI_Chip_Start / _End
Play_Augusta_UI_Weapon_Start / _End
```

角色之间替换的是具体音频内容，而不是重新设计整个调用逻辑。

## 5.13 脚步声：共享原型

公共脚步类型：`BlockHeels`、`Boots`、`Heels`、`MaryJanes`。结构为：

```text
角色 → 鞋型或脚步原型 → 动作速度 → 地面材质 → 共享脚步容器
```

同时存在 `Role_Footstep_...` 与 `Seq_Footstep_...`：Sequence 保留独立脚步接口，让剧情演出不依赖 Gameplay 角色控制逻辑。

## 5.14 `External`：字幕和 Ducking 策略接口

```text
play_external_vo_bubble_hard_ducking
play_external_vo_bubble_soft_ducking
play_external_vo_subtitle_assist
play_external_vo_subtitle_normal
```

VO 系统还管理字幕显示方式、辅助字幕、强弱 Ducking、特殊气泡对白。所以 `VO` 不只是 Voice File，而更接近 **Voice Presentation System（语音呈现系统）**。播放重要语音时系统需要：压低音乐、切换无人声音乐版本、降低环境声音、对白结束后恢复状态。

---

# 第六部分　声音职责层：BAT、AM 与分布式技能事件图

## 6.1 `BAT`：战斗内容总包

`BAT` 横跨 `Role`、`Mon`、`Boss`，内部通常包含 Attack、Skill、Burst、QTE、BeHit、Death、Paralysis、Stand、Walk。高置信度解释：

```text
BAT = Battle / Battle Audio Package（战斗内容总包，不是某一种声音）
```

## 6.2 `AM`：动画同步音频包

`AM` 出现在 `Play/Augusta/AM`、`Mon/Gulong/BAT/AM`、`Role/Jinxi/Anim/AM`，内部出现 `Start`、`End`、`Impact`、`Whoosh`、`FallImpact`、`Far`、`Local`、`Left`、`Right`、`Combo`。结合其他分支明确存在的 `Start_Montage`、`R_Montage`、`B_Montage`，最合理的解释：

```text
AM = Animation Montage（高置信度推断）
或保守表述：与动画时间轴或 Montage 对齐的精细音频同步包
```

## 6.3 一个技能 = 一张分布式声音事件图

以 Augusta 的 `Attack03` 与忌炎的 `Akt03` 为例，一个完整战斗技能可能被拆成：

```text
技能开始
│
├── BAT：战斗动作主体
├── AM：动画同步节点
├── Foley：身体、衣物、武器操作
├── Whoosh：快速挥动
├── FX：能量与视觉特效
├── VO：喊声、呼吸、吼叫
├── Projectile：投射物飞行
├── Hit：攻击命中
├── IMP：冲击层
├── BeHit：目标受击状态
└── End / Tail：动作结束
```

不同节点由不同系统触发：

| 声音节点 | 可能的触发源 |
|---|---|
| 技能主体 | Gameplay Ability |
| Foley / Whoosh | Animation Notify |
| Montage 段落 | Montage Notify |
| 投射物飞行 | Projectile Actor |
| 命中 | Collision / Hit Result |
| 受击 | 目标状态机 |
| FX 层 | Niagara / VFX Timeline |
| VO | 角色行为或概率系统 |
| 阶段切换 | Boss State Machine |

> **战斗音频是多个系统共同调用多个小 Event，在运行时叠加成一个完整技能声音**——不是"按一下技能 → 播放一个巨大音频文件"。

## 6.4 声音层职责总表

| 标签 | 核心含义 | 典型内容 |
|---|---|---|
| `BAT` | 战斗内容总包 | 攻击、技能、QTE、死亡 |
| `AM` | 动画同步包 | 动作内部精确同步点 |
| `Foley` | 角色和装备动作 | 衣物、身体、拔刀、挥臂 |
| `Whoosh` | 高速运动 | 刀剑、肢体、能量掠过 |
| `Hit` | 攻击命中结果 | 武器、元素、强度、距离 |
| `BeHit` | 受击者行为 | 格挡、击飞、倒地、受击 VO |
| `IMP` | 独立冲击 Stem | 轻、中、重冲击 |
| `FX` | 技能与视觉效果 | 能量、爆炸、范围、持续层 |
| `VO` | 发声行为 | 攻击、死亡、警戒、吼叫 |
| `UI` | 界面与展示 | 武器、属性、共鸣、芯片 |

### `Hit` / `BeHit` / `IMP` 的区别（不能统一归为"命中音效"）

```text
Hit   = 攻击者的攻击成功接触目标时播放什么
BeHit = 目标作为受击者进入什么反馈状态
IMP   = 可以与其他声音叠加的冲击声音部件
```

## 6.5 Boss 攻击是动作声音包，不是一条声音

飞廉的 `Atk01` 被拆成 `Atk01_1` ～ `Atk01_7`、`Atk01_VO`，其他攻击还出现 `1_VO`、`2_VO`、`Start`、`Loop`、`End`、`Death`、`Paralysis`、`Phase`、`Walk_F`、`Walk_R`。

**`P1～P10` 不能直接解释成 Boss 阶段**：同一系统明确存在独立的 `Phase`、`Stage1～3`、`Stage1To2`（如 `play_boss_feilian_bat_phase`）。因此 `P1～P10` 更可能是 Part / Point / 内部动作段落 / Montage Notify Point / 声音同步点编号（强推断，正式全称无法从目录证明）。

---

# 第七部分　修饰维度：动作的最后若干 Token

事件名末尾经常不是新动作，而是动作的维度：

| 维度 | Token |
|---|---|
| 时间阶段 | `Pre`、`BuildUp`、`Cast`、`Start`、`Loop`、`End`、`Tail` |
| 距离空间 | `Far`、`Local`、`Near`、`Long`、`Mid`、`Short` |
| 方向 | `L`、`R`、`Left`、`Right`、`Front`、`Back` |
| 强度 | `Light`、`Mid`、`Heavy`、`L1`～`L4` |
| 动作形态 | `EX`、`PRO`、`SP`、`Burst`、`Hold`、`Air` |
| 状态值 | `Stage1～3`、`Normal`、`Danger`、`Safe`、`Silence`、`None` |
| Cue 编号 | `P1`、`P2`、`1Z`、`2A`、`2B`、`4C` |

距离/空间 Token 可能用于：玩家与声源距离差异、角色本地监听者版本、镜头演出版本、大型 Boss 局部身体部位、近身反馈（古龙同一攻击同时存在普通、远距和局部版本）。

## 7.1 呈现层：`nosub`、`amb`、`2d`、`3d`

这些 Token 不描述台词内容，而描述声音如何进入游戏：

- **`nosub`**：不使用常规字幕呈现（环境对白、远处喊话、背景群众、不进正式对话 UI 的声音）；
- **`amb`**：环境式播放版本（3D 定位、距离衰减、环境 Bus、虚声管理、不同优先级、不同字幕规则）；
- **`2d` / `3d` / `3d_far`**：同一角色或内容为不同空间表现建立的独立事件（`play_chun_vo_amb_2d_01` / `_3d_01` / `_3d_far`）。

## 7.2 生命周期：`start / loop / end`

用于蓄力、麻痹、飞行、呼吸、旋涡、变身、持续技能、环境演出等持续动作：

```text
paralysis_start → paralysis_loop → paralysis_end
burst_burst01_start → burst_burst01 → burst_burst01_end
```

一次性语音自然结束，不需要 Stop；循环和环境语音必须由游戏逻辑显式清理。这与地图的 `Enter/Exit/Reset`、状态的 `On/Off` 共同构成跨系统生命周期语法。

---

# 第八部分　变体、数字后缀与多义 Token 的判读

## 8.1 数字后缀不能统一理解为"第几条录音"

项目中存在 `atk01`、`atk0301`、`2_10_51`、`01_amb`、`p2`、`a/b/c`、`vo_2`、`02_vo`、`1_1` 等，它们可能分别代表：动作编号、动作子阶段、剧情节点、节点内台词序号、战斗阶段、形态、录音变体、性别版本、左右方向、内容批次、动画阶段。

```text
play_vo_main_rinascita_2_12_49_nosub_01_f / _01_m   → 末尾 f/m 很可能是女性/男性版本
play_favor_vo_jianxin_atk01_01                       → 01 更像录音变体
```

必须使用分支上下文判断。

## 8.2 `vo` 在不同位置有不同含义（自动解析最易出错的 Token）

| 位置 | 含义 | 示例 |
|---|---|---|
| 路由 | 内容系统 | `play_vo_anke_atk01` |
| 媒体标记 | 发声媒体 | `play_mon_azizi_attack01_vo` |
| 变体名一部分 | 动作/变体名称 | `jcx_atk01_end_vo1`、`vo2` |
| 空间语音类型 | 完整播放类型组合 | `vo_amb_3d` |

因此不能使用 `if "vo" in tokens: media_type = "voice"` 这种规则，必须结合路径位置和分支语法判断。

## 8.3 语言一般不写入事件名

绝大多数事件是语言中立的（`play_vo_anke_atk01`）；只有少量显式 `play_zh_vo_main_yhx_2_nosub_01`。本地化结构是：

```text
en/ja/ko/zh/play/vo/nvzhu → 内部 Event 文件名完全相同（play_vo_nvzhu_atk01）
```

即：**同一个逻辑 Event 名 → 根据当前语言加载对应 Localized Bank → 播放对应语言媒体**，而不是游戏逻辑分别调用 `Play_ZH_...` / `Play_EN_...`。没有语言 Token ≠ 中文，应解释为 `language-neutral event`；`zh` 分支属于明确的中文专用覆盖。

---

# 第九部分　多代管线共存与生产历史

## 9.1 命名系统揭示的多代共存

相似的角色战斗内容有多种写法：

```text
Play_Role_Jiyan_BAT_...
Play_Augusta_AM_...
Role_Jinxi_Anim__AM_...
Mon_Gulong_BAT_AM_...
Play_Mon_Aisheng_BAT_...
```

攻击同时存在 `Attack / Atk / Akt` 三种写法；同一实体有 `Kanteleila / kanteleila` 大小写并存；明显拼写错误包括 `plau`、`commmon`、`stete`、`sequemce`、`ineract`、`interat`、`mosnter`、`slience`、`vison`、`paralysisl`、`transofrm`、`aattack`、`disslike`。

> 当前 Event 命名不是一个人一次性设计的完整本体，而是**早期模板 + 新角色模板 + Boss 专用模板 + 动画管线 + 特效管线 + 剧情临时接入 + 活动版本 + 自动生成工具 + 人工命名 + 历史兼容**长期叠加的结果。部分错误可能直接继承自上游动画或脚本资产名。

## 9.2 版本号不是简单的资源版本字段

`1_3`～`3_4` 等 Token 可能表示首次制作版本、活动版本、剧情版本、导入批次、临时内容包、历史兼容分区。同一版本 Token 在不同路径中意义可能不同，不应把所有 `3_0` 统一解释为 `content_version = 3.0`。更安全的字段：

```text
version_token_raw / version_semantics / version_confidence
```

## 9.3 从命名反推的五条制作管线

**① 角色模板驱动**

```text
角色设计 → 确定 Gameplay 动作槽位 → 生成 com/atk/skill/sys 事件 → 录音填充 → 多语言替换
```

**② 怪物动画驱动**

```text
怪物动画/行为树 → 动作资产命名 → 建立同名 VO 事件 → 动画通知调用
```

**③ 剧情节点驱动**

```text
剧情或任务节点 → 内容包和节点 ID → 生成多个台词实例 → 按呈现需要增加 nosub/amb 版本
```

**④ NPC 原型池驱动**

```text
年龄＋性别原型 → 选择 A/B 声线包 → 按编号调用通用台词
```

**⑤ 技术音频编排**

```text
对白开始 → 播放 VO → 设置 Ducking/字幕/音乐状态 → 管理持续播放 → Stop 并恢复混音
```

---

# 第十部分　生命周期与事件配对关系

## 10.1 值得自动识别的事件配对

| 配对类型 | 结构 |
|---|---|
| 地图生命周期 | `Base ↔ Enter ↔ Exit ↔ Reset` |
| 持续声音 | `Start ↔ Loop ↔ End` |
| 二元控制 | `On ↔ Off`、`Enable ↔ Disable`、`Mute ↔ Unmute`、`Pause ↔ Resume` |
| 播放控制 | `Play ↔ Stop` |
| 状态恢复 | `具体状态 ↔ None`、`具体音乐状态 ↔ Silence` |
| 语音呈现 | `normal ↔ amb`、`male ↔ female` |
| 包装与变体 | `运行时包装事件 ↔ favor 直接变体` |

这些关系对发现缺失 Event、死循环和状态泄漏非常有价值。

## 10.2 VO 特有的关系类型

```text
play_to_stop          （content_key 可计算：去掉 play_/stop_ 前缀即配对）
normal_to_amb
male_to_female
start_to_loop / loop_to_end
form_variant          （humanform ↔ mechaform）
runtime_wrapper_to_direct_variant   （play_vo_jianxin_atk01 ↔ play_favor_vo_jianxin_atk01_01）
```

---

# 第十一部分　怎样正确阅读一个鸣潮事件名（实例集）

**示例一：角色形态技能**

```text
play_vo_aimisi_mechaform_skill_boost_start
play       播放
vo         通用VO系统
aimisi     角色
mechaform  机械形态
skill      技能域
boost      加速／推进动作
start      开始阶段
```

**示例二：档案试听变体**

```text
play_favor_vo_jianxin_atk01_03
play       播放
favor      角色档案／好感系统
vo         VO媒体路由
jianxin    角色
atk01      第一攻击槽位
03         第三个可直接访问变体
```

**示例三：Boss 战斗语音（不可武断拆解）**

```text
play_boss_qunnie_bat_behit_block_01_01_vo
play        播放
boss        Boss事件路由
qunnie      实体
bat         战斗域
behit       受击
block       格挡相关
01_01       动作阶段／变体组合，确切字段未知
vo          发声媒体
```

**示例四：剧情节点环境版**

```text
play_vo_main_linaxita_2_10_51_nosub_01_amb
play        播放
vo          VO路由
main        主线
linaxita    地区／篇章
2_10_51     内容节点
nosub       无常规字幕
01          节点内实例
amb         环境式播放版本
```

**示例五：混音状态控制**

```text
set_scene_music_yrsj_night_no_vocal
set         设置
scene       场景上下文
music       音乐目标
yrsj_night  具体音乐或场景标识
no_vocal    切换到无人声状态
```

**示例六：循环语音生命周期**

```text
stop_vo_mon_wumingtansuozhe_breath_loop_heavy
stop                 停止
vo                   VO路由
mon                  怪物内容
wumingtansuozhe      实体
breath               呼吸
loop                 循环播放
heavy                重型／强烈版本
```

---

# 第十二部分　数据库设计：统一本体

不要只建一张"事件表"。合并两份文档的建议，至少拆成以下结构。

## 12.1 事件主体 `event`

```json
{
  "event_name_raw": "play_role_jiyan_bat_akt03_foley01",
  "operation": "play",
  "owner_domain": "role",
  "package_owner_raw": "jiyan",
  "package_owner_canonical": "character.jiyan",
  "pipeline_package_raw": "bat",
  "pipeline_package_probable": "battle",
  "action_raw": "akt03",
  "action_family": "attack",
  "action_index": 3,
  "audio_layer": "foley",
  "audio_layer_index": 1,
  "phase": null,
  "direction": null,
  "distance": null,
  "intensity": null,
  "form": null,
  "state_group": null,
  "state_value": null,
  "sequence_id": null,
  "cue_id": null,
  "version_token": null,
  "deprecated": false,
  "event_role": "runtime_wrapper",
  "language_scope": "neutral",
  "naming_generation": "legacy_flat",
  "raw_tokens": ["play", "role", "jiyan", "bat", "akt03", "foley01"],
  "normalization": {"akt": "attack", "equivalence_verified": false},
  "confidence": {
    "operation": 1.0,
    "owner_domain": 1.0,
    "package_owner": 1.0,
    "pipeline_package": 0.95,
    "action_family": 0.82,
    "audio_layer": 0.98
  }
}
```

## 12.2 事件组 `event_group`

```json
{
  "group_path": "VO/play/favor/vo/jianxin/atk01",
  "group_key": "play_favor_vo_jianxin_atk01",
  "event_count": 3
}
```

## 12.3 事件关系 `event_relation`

```json
{
  "source_event": "play_vo_jianxin_atk01",
  "target_event": "play_favor_vo_jianxin_atk01_01",
  "relation_type": "runtime_wrapper_to_direct_variant",
  "confidence": 0.9
}
```

完整关系图：

```text
Event
├── belongs_to → ContentPackage
├── owned_by → PackageOwner
├── emitted_by → SourceEntity
├── affects → TargetEntity
├── related_to → RelatedEntity
├── expresses → Action
├── has_phase → LifecyclePhase
├── contains_layer → AudioLayer
├── variant_of → Event
├── paired_with → Event        (play_to_stop / start_loop_end / on_off / ...)
├── sets_state → StateValue
├── used_in → Map / Quest / Sequence
└── triggers → WwiseObject
```

## 12.4 实体与枚举本体

```text
Entity          character / monster / boss / npc / map / object / activity / system
ContentPackage  battle / animation / ui / environment / story / sequence / interaction
Action          attack / skill / born / death / patrol / behit / stand / move / state_transition
AudioLayer      foley / whoosh / impact / hit / behit / fx / vo / music / ambience
Lifecycle       pre / cast / start / loop / end / enter / exit / reset
```

## 12.5 Token 标准化 `token_normalization`

```json
{
  "raw_token": "paralysisl",
  "normalized_token": "paralysis",
  "normalization_type": "probable_typo",
  "rename_original": false
}
```

**原始事件名必须永久保留**；标准化只能用于搜索、聚类、数据分析、显示别名、规则匹配。

---

# 第十三部分　基于事件树的质量检查清单

1. **拼写检查**：`Attack/Atk/Akt`、`Interact/Interat/Ineract`、`Sequence/Sequemce`、`Silence/Slience`；
2. **大小写检查**：`Kanteleila/kanteleila`、`Lucy/lucy`、`M3/m3`；
3. **生命周期完整性**：有 `Start` 是否存在 `End`？有 `Enter` 是否存在 `Exit` 和 `Reset`？有 `On` 是否存在 `Off`？
4. **状态恢复检查**：有 `Danger/Stage1/Warm/Sadness` 是否存在 `Safe/None/Normal/Silence`？
5. **孤立事件检查**：是否存在没有同类角色、没有配对 Event、没有所属包的事件？
6. **废弃接口检查**：`Deprecated` Event 是否仍被游戏逻辑引用？
7. **别名冲突检查**：两个拼写不同的实体名是否实际指向同一角色或怪物？
8. **Stop 配对检查**（VO 特有）：每个循环/环境 `play` 是否有对应 `stop`（content_key 可计算配对）？

---

# 第十四部分　证据等级总结

## 已经能够确定

1. `Event/` 与 `VO/` 目录树都是由事件名分词生成的前缀树；
2. Event 全集 24,042 个文件，`play` 占约 88.5%；VO 子集 6,756 个文件，`play` 占约 99.5%；
3. Event 主要按业务调用上下文组织，不按媒体类型组织；
4. 所有明确事件都保留目录的语义顺序（0 例中间字段重排）；
5. 地图使用 Base—Enter—Exit—Reset 生命周期；
6. State Event 表达状态组和值；
7. 战斗动作被拆成多个同步事件；
8. `Start—Loop—End` 是跨系统生命周期语法；
9. VO 全部 10 个 Stop 事件都有可计算配对的 Play；
10. 语言目录不属于 Event 名本身；
11. `Hit`、`BeHit`、`IMP` 具有不同职责；
12. Boss 内容包可以包含其他角色事件；
13. 项目存在多代命名、拼写错误与废弃接口。

## 高置信度推断

1. `BAT` = Battle / Battle Audio Package；
2. `AM` = Animation Montage 或动画同步音频包；
3. `favor` = 角色语音档案界面的录音变体直接访问层；
4. `play_mon` 与 `play_vo_mon` 的区别在事件所有者（怪物系统 vs 通用 VO 系统），不在"是否说人话"；
5. `LevelB` 与 Level Blueprint 或关卡级接入层相关；
6. `Mxxxxx` 与主线内容相关，`Rxxxxx` 与角色剧情相关；
7. `P1～P10` 是动作内部 Part / Point，不是 Boss 阶段；
8. NPC 的 A/B 声线包对应两名配音演员或两套声线；
9. 战斗音频由 Ability、Animation、Collision、VFX 等多系统共同触发。

## 仍然无法由目录证明

1. JSON 中是否保存 Wwise GUID 或 Short ID；
2. 一个 Event 内有多少条 Action、Action 的具体类型与指向的 HIRC Object；
3. Event 属于哪个 SoundBank；
4. 是否设置了 Switch、State、RTPC 或 Bus；
5. `DA、GP、CS、LVA、LVB` 等内部缩写的正式全称；
6. `loop2.json～loop5.json` 的真实用途；
7. Event 实际由 UE 蓝图、C++、Anim Notify 还是 Sequencer 的哪一处调用；
8. `enter_wild_cxs_no_vo` 等孤立事件的确切语义。

---

# 第十五部分　最终认识

《鸣潮》的 Event 系统不是音效文件索引，VO 子系统也不是录音素材库。它们是同一套**音频业务接口层**的两个视角：

```text
AI 状态        → 怪物行为 Event
角色技能        → 战斗和动画同步 Event（BAT + AM + Foley + FX + Hit + IMP + VO）
Boss 动作       → 多个 Cue 与阶段 Event
地图切换        → 生命周期 Event（Base/Enter/Exit/Reset）
剧情节奏        → 音乐和状态 Event（Cue + State + Stinger）
场景资产        → Bed、Emitter 和 Interaction Event
UI 操作         → 标准角色展示 Event
语音呈现        → VO 路由 + favor 变体层 + nosub/amb/2d/3d 呈现层 + 字幕/Ducking 策略
本地化          → 相同逻辑 Event 下替换语言媒体
```

五个核心设计思想：

1. **事件是业务语义接口**：游戏代码请求的是"角色忌炎执行第三段攻击"，不是"播放 xxx.wav"；
2. **事件名承担大量元数据**：操作、业务域、实体、战斗包、动作、阶段、声音层、方向、距离、强度、形态、版本、Cue 编号可以同时编码在一个名称里；
3. **复杂动作由多个小事件组合**：一个技能 = BAT + AM + Foley + FX + Hit + IMP + VO 的分布式事件图；
4. **生命周期比资产名称更重要**：`Enter/Exit/Reset`、`Start/Loop/End`、`On/Off`、`Play/Stop`、`Mute/Unmute` 贯穿地图、状态、音乐、持续技能、UI 和语音；
5. **Event 是游戏与 Wwise 之间的稳定契约**：即使底层声音对象、Random Container、Switch Container 或媒体文件变化，只要 Event 接口不变，游戏逻辑就不需要同步修改。

从这个角度看，24,042 个 Event 与 6,756 个 VO 事件不是孤立声音，而是**"游戏状态与音频响应之间的契约"**——它既是程序接口，也是内容组织方式；既服务运行时，也暴露了音频团队、战斗团队、动画团队、关卡团队、剧情团队和 UI 团队之间的协作边界。
