# LOL 语音事件类型分类总览
> 来源：`lol_vo_events_index.md`  |  总事件数：**4506**  |  分类数：**50**

---

## 一、分类总览

| 序号 | 分类 | 事件数 | 占比 | 核心命名模式 |
|:----:|:-----|-------:|-----:|:------------|
| 1 | **技能施放** | 825 | 18.3% | `{Champion}R_cast{N}D / {Champion}E_cast{N}D` |
| 2 | **首次遭遇** | 653 | 14.5% | `{Champion}Encounter{N}DAsheSkin{N} / {Champion}Encounter{N}DRivenSkin{N}` |
| 3 | **击杀反馈** | 651 | 14.4% | `{Champion}Champion{N}D_{N} / {Champion}{N}DAsheSkin{N}` |
| 4 | **普攻/暴击** | 501 | 11.1% | `{Champion}BasicAttack{N}_cast{N}D / {Champion}BasicAttack_cast{N}D` |
| 5 | **嘲讽互动** | 350 | 7.8% | `{Champion}{N}DProject{N} / {Champion}{N}DYasuoSkin{N}` |
| 6 | **攻击指令** | 227 | 5.0% | `{Champion}{N}DLuxSkin{N} / {Champion}{N}DThreshSkin{N}` |
| 7 | **移动反馈** | 198 | 4.4% | `{Champion}Near{N}D{N}_Chat{N} / {Champion}Far{N}D{N}_Chat{N}` |
| 8 | **Buff/状态变更** | 170 | 3.8% | `{Champion}BonetoothStack{N} / {Champion}InteractionsRiven{N}_OnBuffActivate` |
| 9 | **命中反馈** | 152 | 3.4% | `{Champion}R_hit{N}D / {Champion}W_hit{N}D` |
| 10 | **购买物品** | 148 | 3.3% | `{Champion}Item{N}D{N} / {Champion}Item{N}D` |
| 11 | **角色对话** | 133 | 3.0% | `{Champion}Attack{N}D{N}_Chat{N} / {Champion}Kill{N}D{N}_Chat{N}` |
| 12 | **首次移动** | 52 | 1.2% | `{Champion}Move{N}D{N}_Chat{N} / {Champion}Move{N}DMap{N}` |
| 13 | **附近事件** | 36 | 0.8% | `{Champion}ChampionDeathSoulCollection{N}DAshe / {Champion}ChampionDeathSoulCollection{N}DAurelionSol` |
| 14 | **位置/伪装触发** | 32 | 0.7% | `{Champion}Nexus{N}D / {Champion}Disguise{N}D` |
| 15 | **玩笑互动** | 32 | 0.7% | `{Champion}{N}D_{N} / {Champion}Response{N}DGeneral` |
| 16 | **打野事件** | 31 | 0.7% | `{Champion}Camp{N}DBaron / {Champion}Camp{N}DBrambleback` |
| 17 | **信号反馈** | 30 | 0.7% | `{Champion}{N}DAssistMe / {Champion}{N}DDanger` |
| 18 | **使用物品** | 29 | 0.6% | `{Champion}Item{N}D{N} / {Champion}Item{N}DWard` |
| 19 | **回城动作** | 27 | 0.6% | `{Champion}Little_Recall_effort_{N} / {Champion}{N}D` |
| 20 | **特殊互动** | 27 | 0.6% | `{Champion}_Interactive{N}DChampionSpecific{N} / {Champion}{N}D` |
| 21 | **技能升级** | 21 | 0.5% | `{Champion}{N}DPRank{N} / {Champion}{N}DRRank{N}` |
| 22 | **重生/出生** | 17 | 0.4% | `{Champion}{N}D / {Champion}RRevive_OnBuffCast` |
| 23 | **舞蹈动作** | 14 | 0.3% | `{Champion}Item{N}DPhantomDancer / {Champion}{N}D` |
| 24 | **角色表情** | 14 | 0.3% | `{Champion}{N}_Recall_Effort{N} / {Champion}Poison{N}D` |
| 25 | **大笑反馈** | 12 | 0.3% | `{Champion}_Laugh{N}DGeneral / {Champion}R_laugh` |
| 26 | **团队集结** | 12 | 0.3% | `{Champion}TeamAhead / {Champion}TeamAhead{N}D` |
| 27 | **变身/隐身** | 11 | 0.2% | `{Champion}{N}D / {Champion}Stealth_activate` |
| 28 | **助攻反馈** | 10 | 0.2% | `{Champion}{N}DCaitlyn / {Champion}{N}DGeneral` |
| 29 | **系统/动画** | 9 | 0.2% | `{Champion}_Idle{N} / {Champion}Threshold` |
| 30 | **野怪相关** | 8 | 0.2% | `{Champion} / {Champion}_Attack{N}DGeneral` |
| 31 | **治疗护盾** | 8 | 0.2% | `{Champion}Support / {Champion}Support{N}D` |
| 32 | **落空反馈** | 7 | 0.2% | `{Champion}W_miss{N}D / {Champion}Q_miss{N}D` |
| 33 | **待机空闲** | 6 | 0.1% | `{Champion}{N}D{N} / {Champion}{N}DGeneral` |
| 34 | **升级反馈** | 6 | 0.1% | `{Champion}Up{N}DGeneral / {Champion}Up{N}DEighteen` |
| 35 | **死亡反馈** | 5 | 0.1% | `{Champion}{N}D / {Champion}{N}D_special` |
| 36 | **首杀反馈** | 5 | 0.1% | `{Champion}Blood{N}D / {Champion}FirstBlood{N}D` |
| 37 | **生存反馈** | 5 | 0.1% | `{Champion}{N}DFleeR / {Champion}{N}DFleeRFlash` |
| 38 | **团队目标** | 5 | 0.1% | `{Champion}Objective{N}D / {Champion}Objective{N}DMonster` |
| 39 | **召唤师技能** | 4 | 0.1% | `{Champion}Spell{N}DTeleportAttachedAlly / {Champion}Teleport_Spell{N}DTeleport` |
| 40 | **特殊模式** | 3 | 0.1% | `{Champion}AscendAlly / {Champion}AscendSelf` |
| 41 | **锻造交互** | 3 | 0.1% | `{Champion}Item_humming / {Champion}P_allypurchasesitem` |
| 42 | **连杀反馈** | 3 | 0.1% | `{Champion}{N}DQuadrakill / {Champion}{N}DStarMultikill` |
| 43 | **守卫相关** | 3 | 0.1% | `{Champion}Ward{N}D / {Champion}Kill{N}D` |
| 44 | **低血量** | 2 | 0.0% | `{Champion}Health{N}D / {Champion}Health{N}DGeneral` |
| 45 | **标记系统** | 2 | 0.0% | `P_Mark_Enemy / P_Mark_Self` |
| 46 | **商店交互** | 2 | 0.0% | `{Champion}{N}DClose / {Champion}{N}DOpen` |
| 47 | **角色关联** | 2 | 0.0% | `{Champion}LucianNear_Heal{N}D / {Champion}VolibearNear_FirstMove{N}D` |
| 48 | **表情动作** | 1 | 0.0% | `{Champion}Mastery{N}D` |
| 49 | **建筑摧毁** | 1 | 0.0% | `{Champion}Destroy{N}D` |
| 50 | **终极技能** | 1 | 0.0% | `{Champion}Pentaill{N}D` |

---

## 1. 技能施放（825 个）

### 命名模式

- `{Champion}R_cast{N}D` — 81 个
- `{Champion}E_cast{N}D` — 74 个
- `{Champion}Q_cast{N}D` — 74 个

### 典型示例

- `AatroxE_OnCast`
- `AhriFoxFire_cast3D`
- `AkaliE_cast3D`
- `AkshanE_cast3D`
- `AlphaStrike_cast3D`
- `AnnieR_cast3D`

### 设计意图

英雄释放技能时的语音反馈。`_cast3D` 表示三维空间播放（玩家可听到），`_OnCast` 是事件钩子触发，`_cast2D` 为本地播放。部分技能区分等级（如 `EzrealR_Level1_cast3D`）或目标（如 `BlindMonkWOne_allycast3D`）。

---

## 2. 首次遭遇（653 个）

### 命名模式

- `{Champion}Encounter{N}DAsheSkin{N}` — 7 个
- `{Champion}Encounter{N}DRivenSkin{N}` — 7 个
- `{Champion}Encounter{N}DLeonaSkin{N}` — 6 个

### 典型示例

- `EnemyFirstEncounter2D`
- `FirstEncounter2D`

### 设计意图

英雄首次遇到特定目标（敌方英雄、阵营、皮肤系列、种族）时触发的台词。命名中 `2D` 为本地语音（仅自己听到），`3D` 为空间语音（附近玩家均可听到）。这是LOL角色塑造的核心手段，通过阵营/皮肤/种族标签实现海量条件分支。

---

## 3. 击杀反馈（651 个）

### 命名模式

- `{Champion}Champion{N}D_{N}` — 26 个
- `{Champion}{N}DAsheSkin{N}` — 5 个
- `{Champion}{N}DLeonaSkin{N}` — 5 个

### 典型示例

- `Kill2DDiana`
- `KillingSpree3D`
- `NearbyEnemyKilledChampionKillingSpree`
- `PentaKill3D`
- `Pentakill3D`
- `RExecuteEnemy2D`

### 设计意图

英雄完成击杀后的语音。细分包括：击杀特定英雄（`Kill3DAhri`）、连杀（`Double`/`Triple`/`Quadra`/`Penta`）、终结大杀特杀（`ShutDownKill3D`）、击杀建筑/野怪。`KillChampion3D` 系列为通用击杀台词池，按序号轮播。

---

## 4. 普攻/暴击（501 个）

### 命名模式

- `{Champion}BasicAttack{N}_cast{N}D` — 145 个
- `{Champion}BasicAttack_cast{N}D` — 116 个
- `{Champion}CritAttack_cast{N}D` — 89 个

### 典型示例

- `AhriBasicAttack2_cast3D`
- `AkaliBasicAttack2_cast3D`
- `AkshanBasicAttack2_cast3D`
- `AmumuBasicAttack2_cast3D`
- `AniviaBasicAttack2_cast3D`
- `AnnieBasicAttack2_cast3D`

### 设计意图

普通攻击与暴击动作的语音。`BasicAttack` 通常有 2~4 段变体循环（`BasicAttack2/3/4`），`CritAttack` 为暴击专属。部分英雄对防御塔有独立语音（`Tower_cast3D`）。

---

## 5. 嘲讽互动（350 个）

### 命名模式

- `{Champion}{N}DProject{N}` — 2 个
- `{Champion}{N}DYasuoSkin{N}` — 2 个
- `{Champion}Response{N}DGeneral` — 2 个

### 典型示例

- `JokeTauntResponse3DGeneral`
- `Taunt3D`
- `TauntendedNearby3D`

### 设计意图

对特定英雄、阵营或标签目标使用嘲讽（Taunt）时的台词，以及嘲讽响应（`TauntResponse`）、嘲讽结束（`TauntEnded`）。`Taunt3DAlly` 为对友方嘲讽，`Taunt3DEnemy` 为对敌方嘲讽。

---

## 6. 攻击指令（227 个）

### 命名模式

- `{Champion}{N}DLuxSkin{N}` — 2 个
- `{Champion}{N}DThreshSkin{N}` — 2 个
- `{Champion}Champion{N}DJinxSkin{N}` — 2 个

### 典型示例

- `Attack2D`
- `ChampionAttack2D`

### 设计意图

玩家下达攻击指令时的语音反馈。`Attack2D` 为本地，`Attack3D` 为空间。细分包括：攻击英雄（`AttackChampion`）、攻击小兵（`AttackMinion`）、攻击野怪（`AttackNeutral`）、攻击特定英雄（`AttackSpecific`）、攻击建筑。

---

## 7. 移动反馈（198 个）

### 命名模式

- `{Champion}Near{N}D{N}_Chat{N}` — 71 个
- `{Champion}Far{N}D{N}_Chat{N}` — 49 个
- `{Champion}{N}DKayle{N}_Chat{N}` — 3 个

### 典型示例

- `HasteRun3D`
- `JungleMove2D`
- `LongMove2D`
- `Move2D`
- `WardJump2D`

### 设计意图

英雄移动时的台词池。`Move2D` 为本地短句，`MoveFar2D` 为长距离移动，`MoveNear2D` 为短距离移动，`MoveOrder2D` 为接受移动指令。`_Chat{N}` 后缀表示同一场景下的多句轮播。

---

## 8. Buff/状态变更（170 个）

### 命名模式

- `{Champion}BonetoothStack{N}` — 5 个
- `{Champion}InteractionsRiven{N}_OnBuffActivate` — 4 个
- `{Champion}RUpgrade{N}_OnBuffCast` — 3 个

### 典型示例

- `AnniePassivePrimed_OnBuffActivate`
- `ApheliosPReload_OnBuffCast`
- `AzirObeliskVOAlly_OnBuffCast`
- `CamilleEDash1_OnBuffCast`
- `CamouflageStealth_OnBuffCast`
- `CardmasterStackParticle_OnBuffActivate`

### 设计意图

Buff/Debuff 激活、失效或层数变化时的语音。`_OnBuffActivate` 为获得状态，`OnBuffDeactivate` 为状态消失，`OnBuffCast` 为状态触发。典型如 `AnniePassivePrimed_OnBuffActivate`（安妮被动满层）。

---

## 9. 命中反馈（152 个）

### 命名模式

- `{Champion}R_hit{N}D` — 4 个
- `{Champion}W_hit{N}D` — 3 个
- `{Champion}EMissile_hit{N}D` — 2 个

### 典型示例

- `AhriSeduceMissile_hit3D`
- `AkaliEbattack_hit`
- `AurelionSolPassive_hit`
- `BelvethR_hit3D`
- `CaitlynEMissile_hit3D`
- `DrMundoQ_hit3D`

### 设计意图

技能命中目标时的语音。`_hit3D` 为命中空间音效，`SpellHit` 为特定技能命中事件。部分英雄对命中特定目标有独立语音（如 `SylasR_hit3DGaren`）。

---

## 10. 购买物品（148 个）

### 命名模式

- `{Champion}Item{N}D{N}` — 66 个
- `{Champion}Item{N}D` — 1 个
- `{Champion}Item{N}DAbyssalMask` — 1 个

### 典型示例

- `BuyItem2D`

### 设计意图

购买装备时的语音。`BuyItem2D` 后接物品ID（如 `1001`）或物品英文名。部分核心装备有角色专属台词（如 `BuyItem2DInfinityEdge`）。

---

## 11. 角色对话（133 个）

### 命名模式

- `{Champion}Attack{N}D{N}_Chat{N}` — 26 个
- `{Champion}Kill{N}D{N}_Chat{N}` — 16 个
- `{Champion}LucianNear_FirstMove{N}D{N}_Chat{N}` — 8 个

### 典型示例

- `AttackChampion3DMorgana01_Chat2`
- `ChampionKill3D01_Chat2`
- `Chat3DKayle_FirstEncounter3DKayle`
- `KayleHealsMorgana3D01_Chat2`
- `MorganaE_Chat3DKayle_Spell3DEHitKayle`
- `NearAttack2D01_Chat2`

### 设计意图

两名英雄在同局内互动时的对话系统。`Chat3D{ChampionA}_{Event}{ChampionB}_Chat{N}` 表示 A 对 B 的某事件做出第 N 句回应。这是LOL叙事深度最高的语音系统，通常需要两名英雄同时在场且触发特定条件。

---

## 12. 首次移动（52 个）

### 命名模式

- `{Champion}Move{N}D{N}_Chat{N}` — 20 个
- `{Champion}Move{N}DMap{N}` — 2 个
- `{Champion}Move{N}D` — 1 个

### 典型示例

- `FirstMove2D`

### 设计意图

游戏开局后英雄首次移动时的台词。`FirstMove2D` 为基础，`FirstMove2DAlly{Champion}` 为特定友方在场，`FirstMove2DEnemy{Champion}` 为特定敌方在场，`FirstMove2DMap{N}` 为特定地图。

---

## 13. 附近事件（36 个）

### 命名模式

- `{Champion}ChampionDeathSoulCollection{N}DAshe` — 1 个
- `{Champion}ChampionDeathSoulCollection{N}DAurelionSol` — 1 个
- `{Champion}ChampionDeathSoulCollection{N}DBilgewater` — 1 个

### 典型示例

- `NearbyChampionDeathSoulCollection2DAshe`

### 设计意图

附近发生特定事件时的语音。如 `NearbyChampionDeathSoulCollection2DDarius`（附近英雄死亡，塞拉斯/斯维因等收集灵魂类英雄的反馈）。

---

## 14. 位置/伪装触发（32 个）

### 命名模式

- `{Champion}Nexus{N}D` — 1 个
- `{Champion}Disguise{N}D` — 1 个
- `{Champion}Disguise{N}DAhri` — 1 个

### 典型示例

- `ApproachNexus3D`
- `EnterDisguise2D`
- `Interactive3DEnterEnemyBase`

### 设计意图

进入特定区域或进入/退出伪装状态时的语音。`EnterDisguise2D` 为妮蔻等变身英雄的伪装进入台词，`EnterEnemyBase3D` 为深入敌方基地时的警告/兴奋台词。

---

## 15. 玩笑互动（32 个）

### 命名模式

- `{Champion}{N}D_{N}` — 2 个
- `{Champion}Response{N}DGeneral` — 2 个
- `{Champion}{N}D` — 1 个

### 典型示例

- `Joke3D`

### 设计意图

使用玩笑（Ctrl+1）时的台词及响应系统。`Joke3D` 为主体，`JokeResponse3D` 为附近英雄的回应，`JokeEndedNearby3D` 为玩笑结束后的环境反馈。

---

## 16. 打野事件（31 个）

### 命名模式

- `{Champion}Camp{N}DBaron` — 2 个
- `{Champion}Camp{N}DBrambleback` — 2 个
- `{Champion}Camp{N}DCloudDrake` — 2 个

### 典型示例

- `ClearCamp2DBaron`
- `InitiateCamp2DBaron`
- `JungleCampHarvest`
- `P_Camp_Kill_Enemy`

### 设计意图

打野过程中的语音。`InitiateCamp2D` 为开始攻击野怪营地，`ClearCamp2D` 为清空营地。按野怪类型细分（Baron/Dragon/Gromp 等）。

---

## 17. 信号反馈（30 个）

### 命名模式

- `{Champion}{N}DAssistMe` — 2 个
- `{Champion}{N}DDanger` — 2 个
- `{Champion}{N}DEnemyMissing` — 2 个

### 典型示例

- `AllyPing3DGank`
- `Ping2DAssistMe`
- `TahmKenchNewR_allyping`

### 设计意图

玩家使用信号（Ping）时的语音反馈。`Ping2DAssistMe` 为请求协助，`Ping2DDanger` 为危险警告，`Ping3DEnemyMissing` 为敌人消失。

---

## 18. 使用物品（29 个）

### 命名模式

- `{Champion}Item{N}D{N}` — 15 个
- `{Champion}Item{N}DWard` — 3 个
- `{Champion}ItemGroup{N}DWard` — 2 个

### 典型示例

- `DestroyItem2DWard`
- `UseItem2D`

### 设计意图

使用消耗品或主动装备时的语音。`UseItem2D` 后接物品ID或名称。`UseItem2DHealthPotion` 为喝药，`UseItem2DWard` 为插眼。

---

## 19. 回城动作（27 个）

### 命名模式

- `{Champion}Little_Recall_effort_{N}` — 5 个
- `{Champion}{N}D` — 2 个
- `{Champion}{N}DGeneral` — 2 个

### 典型示例

- `GnarLittle_Recall_eat`
- `Recall`
- `Skin14_Recall_efforts01`
- `Slayer_RecallLeadOut2D_oncast`

### 设计意图

回城（Recall）过程中的语音。`Recall3D` 为回城主体，`RecallLeadIn3D` 为回城开始前的引导，`RecallWindDown3D` 为回城取消。部分皮肤有专属回城语音（如 `Skin14_Recall_efforts01`）。

---

## 20. 特殊互动（27 个）

### 命名模式

- `{Champion}_Interactive{N}DChampionSpecific{N}` — 6 个
- `{Champion}{N}D` — 1 个
- `{Champion}{N}DAce` — 1 个

### 典型示例

- `Insec2D`
- `Interactive3DAce`
- `RShareGold3D`
- `Special2DWeaponUpgradeFirst`
- `VoidSpawnIn`
- `VolcanoGod_Interactive_Interactive3DReturningToBase`

### 设计意图

特殊机制或模式下的语音。如 `Interactive3DPentakill`（五杀特殊互动）、`Insec2D`（盲僧回旋踢纪念语音）、`WeaponUpgrade`（女枪武装战姬形态切换）。

---

## 21. 技能升级（21 个）

### 命名模式

- `{Champion}{N}DPRank{N}` — 4 个
- `{Champion}{N}DRRank{N}` — 3 个
- `{Champion}{N}DERank{N}` — 1 个

### 典型示例

- `Spell2DERank1`
- `SyndraE_maxskill`

### 设计意图

技能点升级时的语音。`Spell2D{Q/W/E/R}Rank{N}` 为某技能升到第 N 级时的反馈。部分英雄对终极技能（R）首次升级有独立台词。

---

## 22. 重生/出生（17 个）

### 命名模式

- `{Champion}{N}D` — 3 个
- `{Champion}RRevive_OnBuffCast` — 1 个
- `{Champion}{N}DGeneral` — 1 个

### 典型示例

- `AatroxRRevive_OnBuffCast`
- `Respawn2D`
- `Spawn2D`
- `MalzaharRespawn`

### 设计意图

英雄复活或游戏开始时出生点的语音。`Respawn2D/3D` 为复活，`Spawn2D` 为出生。部分皮肤对敌方出生有嘲讽（`SpawnEnemy2D...`）。

---

## 23. 舞蹈动作（14 个）

### 命名模式

- `{Champion}Item{N}DPhantomDancer` — 1 个
- `{Champion}{N}D` — 1 个
- `{Champion}{N}D_Loop_buffactivate` — 1 个

### 典型示例

- `BuyItem2DPhantomDancer`
- `Dance3D`
- `dance_buff`
- `dance_buffactivate`
- `dance_leadin`
- `WithRakanDance3D`

### 设计意图

使用舞蹈（Ctrl+3）时的语音。`Dance3D` 为主体，`Dance3D_loop` 为循环段，`DanceResponse3D` 为附近英雄对舞蹈的回应。

---

## 24. 角色表情（14 个）

### 命名模式

- `{Champion}{N}_Recall_Effort{N}` — 2 个
- `{Champion}Poison{N}D` — 1 个
- `{Champion}Potion{N}D` — 1 个

### 典型示例

- `DrinkPoison3D`
- `EatHoneyFruit2D`
- `Effort3D`
- `Giggle3D01`
- `HypeTrain3D`
- `NeekoR_UltimateEffortCast`

### 设计意图

非语言的角色音效。`Effort3D` 为发力/喘息声，`Giggle3D` 为轻笑，`HypeTrain3D` 为兴奋，`DrinkPoison3D` 为喝药水的声音。

---

## 25. 大笑反馈（12 个）

### 命名模式

- `{Champion}_Laugh{N}DGeneral` — 2 个
- `{Champion}R_laugh` — 1 个
- `{Champion}{N}D` — 1 个

### 典型示例

- `GangplankR_laugh`
- `Laugh3D`
- `laugh3D_in`
- `laugh3D_loop`
- `laugh3Dbase`
- `laugh3Dult`

### 设计意图

使用大笑（Ctrl+4）时的语音。`Laugh3D` 为主体，`Laugh3DGeneral` 为通用，`laugh3D_loop` 为循环笑。

---

## 26. 团队集结（12 个）

### 命名模式

- `{Champion}TeamAhead` — 1 个
- `{Champion}TeamAhead{N}D` — 1 个
- `{Champion}TeamAhead{N}DAlly` — 1 个

### 典型示例

- `RallyTeamAhead`
- `TeamRally3D`

### 设计意图

团队局势相关的鼓舞/泄气台词。`RallyTeamAhead3D` 为领先时鼓舞队友，`RallyTeamBehind3D` 为落后时打气，`TeamRally3D` 为通用集结。

---

## 27. 变身/隐身（11 个）

### 命名模式

- `{Champion}{N}D` — 2 个
- `{Champion}Stealth_activate` — 1 个
- `{Champion}E_StealthExit{N}D` — 1 个

### 典型示例

- `EvelynnStealth_activate`
- `PykeE_StealthExit3D`
- `Transform2D`

### 设计意图

英雄形态切换或进入隐身时的语音。`Transform2D/3D` 为变身（如杰斯/奈德丽），`CamouflageStealth_OnBuffCast` 为伪装触发，`stealthExit3D` 为退出隐身。

---

## 28. 助攻反馈（10 个）

### 命名模式

- `{Champion}{N}DCaitlyn` — 1 个
- `{Champion}{N}DGeneral` — 1 个
- `{Champion}{N}DGraves` — 1 个

### 典型示例

- `Assist3DCaitlyn`

### 设计意图

参与击杀但未拿到人头时的语音。`Assist3DGeneral` 为通用助攻，`Assist3D{Champion}` 为对特定英雄的助攻。

---

## 29. 系统/动画（9 个）

### 命名模式

- `{Champion}_Idle{N}` — 3 个
- `{Champion}Threshold` — 1 个
- `{Champion}_run` — 1 个

### 典型示例

- `AnimalThreshold`
- `Animations_Idle2`
- `cast3D`
- `CloneDestroyed2D`
- `destoryterrain`
- `GunSelect2D`

### 设计意图

底层动画或系统事件触发的语音。`Animations_Idle2` 为待机动画变体，`AnimalThreshold` 为动物阈值（可能为特定彩蛋），`destoryterrain` 为地形破坏。

---

## 30. 野怪相关（8 个）

### 命名模式

- `{Champion}` — 2 个
- `{Champion}_Attack{N}DGeneral` — 1 个
- `{Champion}_Death{N}D` — 1 个

### 典型示例

- `Baron`
- `Dragon`
- `Sentinel_Attack2DGeneral`
- `StealMonster3D`

### 设计意图

与野怪直接相关的非击杀语音。如 `Baron`（男爵环境音）、`Dragon`（龙坑环境）。

---

## 31. 治疗护盾（8 个）

### 命名模式

- `{Champion}Support` — 2 个
- `{Champion}Support{N}D` — 2 个
- `{Champion}WithSennaNear` — 1 个

### 典型示例

- `HealSupport`
- `NearbyEnemyUsedItemHealthPot`
- `Receive3DHealHoneyfruit`
- `ShieldSupport`

### 设计意图

获得治疗或护盾时的语音。`HealSupport3D` 为受到治疗，`Receive3DShieldHeal` 为获得护盾，`ShieldSupport3D` 为提供护盾。

---

## 32. 落空反馈（7 个）

### 命名模式

- `{Champion}W_miss{N}D` — 2 个
- `{Champion}Q_miss{N}D` — 1 个
- `{Champion}W_SpellMissKaisaW` — 1 个

### 典型示例

- `EzrealQ_miss3D`
- `KaisaW_miss3D`
- `TaricE_missilecast`
- `WarwickWActiveMiss`
- `ZeriW_miss3D`
- `ZoeQ_nearmiss`

### 设计意图

技能未命中时的语音。`_miss3D` 为弹道落空，`SpellMiss` 为特定技能未命中，`nearmiss` 为擦身而过。

---

## 33. 待机空闲（6 个）

### 命名模式

- `{Champion}{N}D{N}` — 2 个
- `{Champion}{N}DGeneral` — 2 个
- `{Champion}{N}D` — 1 个

### 典型示例

- `Idle2D01`

### 设计意图

英雄长时间无操作时的待机语音。`Idle2DGeneral` 为通用，`Idle3D` 为空间播放。

---

## 34. 升级反馈（6 个）

### 命名模式

- `{Champion}Up{N}DGeneral` — 2 个
- `{Champion}Up{N}DEighteen` — 1 个
- `{Champion}Up{N}DEleven` — 1 个

### 典型示例

- `LevelUp2DEighteen`

### 设计意图

英雄等级提升时的语音。`LevelUp2DGeneral` 为通用升级，`LevelUp2DSix` 为 6 级（大招解锁）。

---

## 35. 死亡反馈（5 个）

### 命名模式

- `{Champion}{N}D` — 2 个
- `{Champion}{N}D_special` — 1 个
- `{Champion}{N}DRivenSkin{N}` — 1 个

### 典型示例

- `Death3D`
- `Dying3D`

### 设计意图

英雄死亡时的语音。`Death3D` 为通用，`Death3D_special` 为特殊死亡（如被特定英雄击杀）。

---

## 36. 首杀反馈（5 个）

### 命名模式

- `{Champion}Blood{N}D` — 1 个
- `{Champion}FirstBlood{N}D` — 1 个
- `{Champion}FirstBlood{N}DAlly` — 1 个

### 典型示例

- `FirstBlood3D`
- `GotFirstBlood3D`
- `Interactive3DFirstBlood`

### 设计意图

拿到或见证 First Blood 时的语音。`FirstBlood3D` 为自身拿到，`GotFirstBlood3DAlly` 为友方拿到，`GotFirstBlood3DEnemy` 为敌方拿到。

---

## 37. 生存反馈（5 个）

### 命名模式

- `{Champion}{N}DFleeR` — 1 个
- `{Champion}{N}DFleeRFlash` — 1 个
- `{Champion}Standing{N}D` — 1 个

### 典型示例

- `Interactive3DFleeR`
- `LastStanding2D`
- `SurviveJustice3D`
- `TeamFightSurvive2D`

### 设计意图

残血逃生或极限生存时的语音。`SurviveJustice3D` 为丝血反杀，`LastStanding2D` 为最后幸存者。

---

## 38. 团队目标（5 个）

### 命名模式

- `{Champion}Objective{N}D` — 1 个
- `{Champion}Objective{N}DMonster` — 1 个
- `{Champion}Objective{N}DStructure` — 1 个

### 典型示例

- `TeamObjective3D`

### 设计意图

团队完成目标时的语音。`TeamObjective3DMonster` 为击杀史诗野怪，`TeamObjective3DStructure` 为摧毁建筑。

---

## 39. 召唤师技能（4 个）

### 命名模式

- `{Champion}Spell{N}DTeleportAttachedAlly` — 1 个
- `{Champion}Teleport_Spell{N}DTeleport` — 1 个
- `{Champion}Teleport_TeleportAlly{N}D` — 1 个

### 典型示例

- `SummonerSpell3DTeleportAttachedAlly`

### 设计意图

使用召唤师技能时的语音。`SummonerTeleport_TeleportAlly2D` 为传送友方时的反馈。

---

## 40. 特殊模式（3 个）

### 命名模式

- `{Champion}AscendAlly` — 1 个
- `{Champion}AscendSelf` — 1 个
- `{Champion}Kill{N}DWhileAscended` — 1 个

### 典型示例

- `AscensionAscendAlly`

### 设计意图

特殊游戏模式专属语音。`AscensionAscendAlly` 为飞升模式友方飞升。

---

## 41. 锻造交互（3 个）

### 命名模式

- `{Champion}Item_humming` — 1 个
- `{Champion}P_allypurchasesitem` — 1 个
- `{Champion}P_finishforging` — 1 个

### 典型示例

- `ForgeItem_humming`
- `OrnnP_allypurchasesitem`

### 设计意图

奥恩锻造系统专属语音。`ForgeItem_humming` 为锻造时的哼唱，`OrnnP_finishforging` 为锻造完成。

---

## 42. 连杀反馈（3 个）

### 命名模式

- `{Champion}{N}DQuadrakill` — 1 个
- `{Champion}{N}DStarMultikill` — 1 个
- `{Champion}MultiKill{N}D` — 1 个

### 典型示例

- `Interactive3DQuadrakill`
- `UltimateMultiKill3D`

### 设计意图

连续击杀时的语音。`Kill3DDouble`/`Triple`/`Quadra`/`Penta` 为连杀播报。

---

## 43. 守卫相关（3 个）

### 命名模式

- `{Champion}Ward{N}D` — 2 个
- `{Champion}Kill{N}D` — 1 个

### 典型示例

- `PlaceWard2D`
- `UseWard2D`
- `WardKill2D`

### 设计意图

与眼/守卫相关的语音。`PlaceWard2D` 为插眼，`WardKill2D` 为排眼，`UseItemWard2D` 为使用守卫。

---

## 44. 低血量（2 个）

### 命名模式

- `{Champion}Health{N}D` — 1 个
- `{Champion}Health{N}DGeneral` — 1 个

### 典型示例

- `LowHealth2D`

### 设计意图

生命值过低时的警告/自嘲语音。`LowHealth2DGeneral` 为通用低血量。

---

## 45. 标记系统（2 个）

### 命名模式

- `P_Mark_Enemy` — 1 个
- `P_Mark_Self` — 1 个

### 典型示例

- `P_Mark_Enemy`
- `P_Mark_Self`

### 设计意图

标记敌人或自身时的语音。`P_Mark_Enemy` 为标记敌方，`P_Mark_Self` 为标记自身。

---

## 46. 商店交互（2 个）

### 命名模式

- `{Champion}{N}DClose` — 1 个
- `{Champion}{N}DOpen` — 1 个

### 典型示例

- `Shop2DClose`

### 设计意图

打开/关闭商店时的语音。`Shop2DOpen`/`Shop2DClose`。

---

## 47. 角色关联（2 个）

### 命名模式

- `{Champion}LucianNear_Heal{N}D` — 1 个
- `{Champion}VolibearNear_FirstMove{N}D` — 1 个

### 典型示例

- `WithLucianNear_Heal2D`

### 设计意图

特定英雄在附近时触发的关联语音。`WithLucianNear_FirstMove2D` 为赛娜与卢锡安同队时的首次移动台词。

---

## 48. 表情动作（1 个）

### 命名模式

- `{Champion}Mastery{N}D` — 1 个

### 典型示例

- `FlashMastery3D`

### 设计意图

使用表情（Mastery）时的语音。`FlashMastery3D` 为亮标。

---

## 49. 建筑摧毁（1 个）

### 命名模式

- `{Champion}Destroy{N}D` — 1 个

### 典型示例

- `TowerDestroy2D`

### 设计意图

摧毁建筑时的语音。`KillTurret3DTowerDestroy` 为拆塔。

---

## 50. 终极技能（1 个）

### 命名模式

- `{Champion}Pentaill{N}D` — 1 个

### 典型示例

- `UltimatePentaill3D`

### 设计意图

终极技能专属 effort 语音。`UltimateEffort3D` 为释放大招时的蓄力/呐喊声。

---
