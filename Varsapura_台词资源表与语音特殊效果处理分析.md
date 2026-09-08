 # 《Varsapura》台词表与特殊效果处理分析

---

## 核心设计哲学

《Varsapura》的语音设计不是先想"加什么效果"，而是先追问**声音为何存在、通过什么机制发出、玩家为什么需要听见**，再从角色、空间、媒介和剧情状态推导处理：自然人声锚定现实，广播与通讯建立城市秩序，声像移动、叠声和失真赋予异常可信的存在方式；同时用有限效果、状态变化和适时留白保护表演，让每个声音都服务于叙事与世界。

### 声音的三层现实

|       层级       | 代表角色                                                             | 核心特征                                                                                                |
| :------------: | :--------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| **第一层：现实人物声**  | Receptionist、Male Applicant、Player现场声、Sayuki现场声                  | 单声道角色素材，绑定嘴部或角色Emitter，由引擎计算方向与距离，服从房间反射、遮挡和玩家镜头，尽量保留演员本体。这层声音是**现实锚点**，告诉玩家：这里仍是一个可以依靠普通物理规律理解的空间。 |
| **第二层：机构媒介声音** | Safety Exhibit、Announcement System、Simmons、Dispatch、DAWN、SEAL HQ | 声音**必须经过某个机构媒介才能抵达玩家**。不同媒介代表不同权力结构，媒介质感实际上是**组织结构的声音化**。                                           |
| **第三层：异常意识声音** | Mr. Shadow、Vivian、Mindbog Thought                                | 共同破坏"声音必然来自一个身体和位置"的日常规则，让"异常"不只存在于怪物视觉中，而直接进入玩家对空间和主体的判断。                                          |

---

### 机构媒介的权力映射

| 声音来源 | 机构意义 |
|:---|:---|
| **Safety Exhibit** | 官方把异常转化为公共安全知识 |
| **Announcement System** | 机构用编号和流程管理个体 |
| **Simmons／Sayuki通讯** | 后方技术与前线行动连接 |
| **Dispatch Center** | 镜头外的整座城市仍在同时运行 |
| **SEAL HQ** | 组织拥有宣布全局状态的权力 |
| **DAWN** | 教程、权限、观察和陪伴被整合成系统人格 |

---

### 异常意识的四种破坏方式

| 声音 | 破坏的关系 |
|:---|:---|
| **Mr. Shadow** | 有稳定人格，却没有稳定位置 |
| **Vivian** | 似乎有人格，但声音和身体都没有完全进入现实 |
| **Mindbog Thought** | 有语言内容，却没有单一说话人 |
| **Player内心声** | 有明确主体，但没有外部空气声源 |

---

### 设计原则：先解释发生了什么，再设计声音

分析《Varsapura》时，应先问：

- Mr. Shadow 为什么无法稳定定位？
- Mindbog 里的辱骂属于谁的思想？
- Vivian 为什么同时在声音与画面上不完整？
- DAWN 是现场智能、录音档案，还是二者共用的系统人格？
- Simmons 和 Sayuki 为什么使用同一种通讯声纹？

> **正确链路：** 世界设定 → 发声机制 → 传播媒介 → 接收权限 → 空间关系 → 声音处理
>
> **错误链路：** 神秘角色 → 加反向混响；强大角色 → 加低八度；机械角色 → 加失真

---

## 特殊效果处理规范

> 核心不是"用了哪些插件"，而是：**先判断声音在世界中是什么、从哪里来、谁能听见，再决定它应该怎样响。**

---

### 一、机构媒介声音处理

> 共同特点不是某一种滤波，而是：**声音必须经过某个机构媒介才能抵达玩家。**
>
> 这里的 EQ、压缩和设备染色并非为了让声音"更酷"，而是在告诉玩家：**这句话经过了什么机构、什么设备和什么权限网络才抵达你。**媒介质感因此成为世界观的一部分。

---

#### **FX-B1｜安全展示装置／电话式设备染色**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 单声道旁白素材 |
| **最终输出声场** | 固定设备点声源的空间化输出 |
| **具体处理** | 使用 EQ 收窄频段并加入设备染色，再绑定展示装置位置进行 3D 空间化 |
| **判断** | 重点是设备播放质感，不是普通广播，也不是贴耳教程旁白 |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Safety Exhibit Narrator** | Although organic matter is more resistant to decomposition, Mind Rot can severely affect mental health. If exposed, seek medical help immediately. Rest assured, our MRP officers will clear affected areas and reverse the Mind Rot's effect on your property. |
| **Safety Exhibit Narrator** | Welcome. You're about to observe the process of mind rotting. Note the black substance seeping from the object. This is Mind Rot. |

---

#### **FX-B2｜清晰型大厅 Broadcast**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 很可能是单声道广播素材 |
| **最终输出声场** | 空间化立体声大厅声场 |
| **具体处理** | 保留清晰、明亮的高频和高可懂度；叠加大厅混响，并通过 PA 位置或多扬声器覆盖形成空间感 |
| **判断** | 虽然存在大厅混响，但不是遥远、浑浊的老旧喇叭声；核心仍是清楚地引导玩家 |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Announcement System** | Number I-07, please proceed to the interview room, down the hall on the left of the front desk. |

---

#### **FX-E1｜SEAL 内部通讯／Simmons 与 Sayuki 共用**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 单声道人声素材 |
| **最终输出声场** | 中心化、非环境定位的通讯输出 |
| **具体处理** | 统一通讯 EQ、明显动态压缩和稳定电平，突出力量与可懂度 |
| **判断** | Simmons 与远程指导阶段的 Sayuki 使用同一套通讯效果，不再拆成两种 Preset |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Simmons** | DAWN authorization approved. Personnel permitted: two. Preparing the test chamber. Marsha is waiting for you. |
| **Simmons** | Fine. Seems like replicator number three needs a lens adjustment. |
| **Simmons** | She won't go easy on you. Good luck. |
| **Sayuki（通讯）** | You've got 60 seconds to eliminate the approaching Shadow Monsters. Good luck. Swift and precise. Good job. On to the next one. That was just a basic drill. Fieldwork requires quick action, but remember, speed is secondary to ensuring the safety of civilians. Time for your second trial. Save the civilians without alerting the monsters. Keep a low profile and stay undetected. Use your abilities when needed. Great job. Go through that door and catch your breath. You've earned it. |
| **Simmons（通讯）** | The exit's blocked and there's Mind Rot in the chamber. Don't touch it if you want to live. Just opened a new route for you. Up you go. Take the stairs. Run quickly. |
| **Simmons（通讯）** | Mind Rot readings are off the charts. Any trouble downtown? |
| **Sayuki（通讯）** | Yeah, there's a Code Red in Oakwood District. Can you let the rookie out? |
| **Simmons（通讯）** | Already on it. I've got more of these bastards to deal with. The exit route is at 60%. Try to keep it together in the meantime. |
| **Simmons（通讯）** | Where are you going? |
| **Simmons（通讯）** | The route's unstable. You'll be trapped inside, too. |
| **Simmons（通讯）** | Damn. The chamber's unstable, but I'll get you out. |
| **Simmons（通讯）** | Anyone hurt? |
| **Simmons（通讯）** | There's a full response underway. Patrol needs you. |

---

#### **FX-E2｜SEAL 通讯的异常干扰状态**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 沿用 SEAL 内部通讯素材 |
| **最终输出声场** | 中心通讯声，但稳定性下降 |
| **具体处理** | 在共用通讯效果之上增加断续、失真、频段缺失或信号不稳定 |
| **判断** | 它是同一通讯系统的状态变体，不应视为 Simmons 的新角色声纹 |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Simmons（受干扰通讯）** | Exit's almost open. Just hold on. Command invalid. Now, be careful. It's getting closer. |
| **Simmons（受干扰通讯）** | Deploying platforms. |

---

#### **FX-F1｜车载双向无线电／调度信道**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 单声道通讯素材 |
| **最终输出声场** | 车内设备播放；中心或近中心 |
| **具体处理** | 使用无线电带宽、压缩、轻度通讯染色，并通过车内扬声器或通讯设备播放 |
| **判断** | Dispatch Center、Finn 与 Valentina 属于同一套车载通讯效果；差异主要来自说话人与调度／前线身份 |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Dispatch Center** | Boyce Park, ready for cleanup. |
| **Finn（通讯）** | Finn here. On the scene now. |
| **Dispatch Center** | Requesting additional S.U.N. response in Oakwood. |
| **Valentina／V（通讯）** | This is V. Be there soon. |
| **Dispatch Center** | Pruden Hill is expanding. Code Yellow. Looks like someone's already flagged it. |

---

#### **FX-G1｜DAWN 车载终端／Training Tapes 播放声**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 单声道 DAWN 语音 |
| **最终输出声场** | 车载终端／设备播放声场 |
| **具体处理** | DAWN 培训模块和实时助手共用相近的设备 EQ 与染色；培训内容前可加入提示音或播放启动感 |
| **判断** | Training tapes 明确说明是预录培训媒体，但单凭这个词不能证明使用了真实磁带 Wow／Flutter；当前更稳妥地称为磁带式或档案式设备播放 |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **DAWN（培训模块）** | As you've learned, humanity's collective thoughts manifest as the Rain of Thought. Like water stagnating without proper drainage, it can build up and cause rot. Mind Rot buildups corrode reality, breaking minds, spawning monsters, and warping our world. End of module 14. Proceed to— |
| **DAWN** | Permission updated. Access granted. Hello, Rookie. I'm DAWN, SEAL's companion. |
| **DAWN** | Yes. Ready to locate nearby monsters. Always a pleasure. Happy to work with everyone's favorite SEAL officer. It looks like that ad campaign is really— |

---

#### **FX-I1｜SEAL 全单位优先广播**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 单声道机构播报素材 |
| **最终输出声场** | 通讯／广播声场 |
| **具体处理** | 保持稳定响度和极高可懂度，作为系统级状态播报覆盖行动场景 |
| **判断** | 属于组织范围的优先广播，不等同于大厅 PA |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **SEAL HQ（全单位广播）** | Attention all units. Oakwood has been contained. Emergency status lifted. You may resume regular duties. |

---

### 二、异常意识声音处理

> 它们共同破坏"声音必然来自一个身体和位置"的日常规则，但破坏方式不同。这让"异常"不只存在于怪物视觉中，而直接进入玩家对空间和主体的判断。

---

#### **FX-C1｜Mr. Shadow 基础异常声／轻微动态立体声**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 源素材形态无法仅凭成片确定 |
| **最终输出声场** | 轻度立体声；声像持续变化 |
| **具体处理** | 保持主体台词清晰，同时让左右位置、宽度、层间比例或空间返回缓慢变化 |
| **判断** | 能确定的是动态声像；无法仅凭听感断定使用了 Pan、Doubler、叠层还是混响返回自动化 |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Mr. Shadow** | Yet another Hollowone. |
| **Mr. Shadow** | Your straw-filled mind wanders the wasteland inside. Still, you're haunted by a nameless lie. You don't know who you are. I see your true self. You're no hero. |
| **Mr. Shadow（异常空间声）** | Including you if you stay here. Now, go. |
| **Mr. Shadow（异常空间声）** | I will take it from here. Hollowone, with me. |
| **Mr. Shadow** | The situation is serious, but they have what it takes. As for you, I'm humbled. Even an entity like me can misjudge your potential. It runs deeper than you realize. But your motivations are not as they appear. Correct? |
| **Mr. Shadow** | While unofficial, this conversation will determine your future with the Bureau. Why do you want to join SEAL? |
| **Mr. Shadow** | Not the most altruistic goal. |
| **Mr. Shadow** | A fair point. We share the same goals. You have a way with words. The Bureau needs your help with the Mind Rot incident. Prove yourself worthy of this. |
| **Mr. Shadow** | Oh? Why the sudden interest? |
| **Mr. Shadow** | Expressing gratitude, what a rare trait. I'll help you. Await my message. |

---

#### **FX-C3｜Mr. Shadow 左→右空间混响扫动**

> Mr. Shadow 的处理没有只依赖低八度、重失真或传统恶魔声。其核心是**"声音无法保持稳定的位置"**。
>
> 效果不是持续堆满，而是有收、有放、有例外：
> - **动态立体声** → 表达"他无法被稳定定位"
> - **中置** → 表达"他已经作出判断"
> - **横向扫动** → 表达"他的影响仍残留在空间里"
>
> 同一个声纹系统因此能够参与句子语义和段落结构。

| 项目 | 内容 |
|:---|:---|
| **素材声道** | Mr. Shadow 主体声 |
| **最终输出声场** | 立体声；由左向右运动 |
| **具体处理** | 对白主体与空间混响共同完成横向扫动，句尾保留空间尾音 |
| **判断** | 这是"Welcome to SEAL"的单句强调效果，**不应套用到 Mr. Shadow 所有对白** |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Mr. Shadow** | Welcome to SEAL. |

---

#### **FX-D1｜Vivian 尖锐粒子化异常声**

> **强烈失真人格残影**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 未知 |
| **最终输出声场** | 模糊、非稳定定位的立体声感 |
| **具体处理** | 强化尖锐感、破碎感与难辨认度，使声音与虚化、粒子化的人物画面一致 |
| **判断** | 她不是普通现场 NPC 声；**听不清本身就是异常呈现的一部分** |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Vivian** | （台词内容无法清晰辨认） |

---

#### **FX-D2｜Mindbog Thought 精神侵入复合声**

| 项目 | 内容 |
|:---|:---|
| **素材声道** | 可能由多层单声道人声构成 |
| **最终输出声场** | 宽立体声／非固定位置 |
| **具体处理** | 保留可懂主声，叠加微时差、微音高差、Doubler 或合唱式副层，并让左右层不同步 |
| **判断** | 听感接近《沙丘》The Voice 式多层压迫，但其叙事身份是 Mindbog 中的思想侵入 |

**需要处理的台词：**

| 说话人 | 台词 |
|:---|:---|
| **Unknown Voice／Mindbog Thought** | Go to hell! Hideous freak! You're worthless! |

---

## 完整台词总表

> 按剧情流程分章，每章内以表格形式列出说话人、台词、声道格式、引擎空间化需求及对应效果编号。

---

### 第一章：开场、申请与大厅

| 说话人 | 具体台词 | 单声道／立体声 | 引擎空间化 | 特殊效果 |
|:---|:---|:---:|:---:|:---|
| **Player／Hollowone（旁白）** | If you've been suffering from insomnia, nightmares, or mood swings, you may find these images unsettling. Back then, I had no idea. Maybe that wasn't the real me. | 单声道（中置） | — | — |
| **Receptionist** | You lost belongings due to Mind Rot? Please visit that counter over there, Mind Rot Control. | 单声道 | ✓ | — |
| **Male Citizen** | All right, thanks. | 单声道 | ✓ | — |
| **Receptionist** | How can I help you? | 单声道 | ✓ | — |
| **Player／Hollowone** | Um, I'd like to join SEAL. | 单声道 | — | — |
| **Receptionist** | Okay. You'll need to go through the interview process first. This is your application form. Read the instructions and sign to confirm. Once you sign, we'll verify your consciousness. This may cause slight discomfort. Let me see. Consciousness verification completed. Preparing the interview. Your number, I-07. They'll call it out through the announcement system, so please pay attention. It may take a moment. This area is open to visitors. Feel free to look around while you wait. | 单声道 | ✓ | — |
| **Safety Exhibit Narrator** | Although organic matter is more resistant to decomposition, Mind Rot can severely affect mental health. If exposed, seek medical help immediately. Rest assured, our MRP officers will clear affected areas and reverse the Mind Rot's effect on your property. Welcome. You're about to observe the process of mind rotting. Note the black substance seeping from the object. This is Mind Rot. | 单声道 | ✓ | **FX-B1** 电话式 EQ／设备染色 |
| **Announcement System** | Number I-07, please proceed to the interview room, down the hall on the left of the front desk. | 立体声 | ✓ | **FX-B2** 明亮高频／大厅混响 |

---

### 第二章：候选人闲聊与 Mr. Shadow 面试

| 说话人 | 具体台词 | 单声道／立体声 | 引擎空间化 | 特殊效果 |
|:---|:---|:---:|:---:|:---|
| **Male Applicant** | You're here for an interview? | 单声道 | ✓ | — |
| **Player／Hollowone** | Yeah. Hi. Uh... | 单声道 | ✓ | — |
| **Male Applicant** | Well, isn't that something? They really hit the jackpot with candidates like us. Come on. Take a seat. There's only so many safety brochures to leaf through. Grab a chair. Let's chat for a bit. This whole Shadow Bureau seems so shady. Everyone says they're strict about hiring, but there are no clear standards. They don't even accept resumes. I don't even know how to prepare. But it's not like I have no experience, you know? I've watched Mindbog Murders and Shadow Boys several times. Nothing I can't handle. | 单声道 | ✓ | — |
| **Player／Hollowone** | What's up with the lights? | 单声道 | ✓ | — |
| **Male Applicant** | What do you think is the better pick? Rescue Brigade or S.U.N.? | 单声道 | ✓ | — |
| **Player／Hollowone** | Did you see that? | 单声道 | ✓ | — |
| **Male Applicant** | Huh? Maybe the Brigade? My girlfriend thinks they're hot. | 单声道 | ✓ | — |
| **Player／Hollowone** | Uh... What happened? Hello? Um, hello? | 单声道 | ✓ | — |
| **Mr. Shadow** | Yet another Hollowone. | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Player／Hollowone** | A Hollowone? What? | 单声道 | ✓ | — |
| **Mr. Shadow** | Your straw-filled mind wanders the wasteland inside. Still, you're haunted by a nameless lie. You don't know who you are. I see your true self. You're no hero. | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Mr. Shadow** | I'd say average at best. An officer has come to collect you. | 单声道（中置） | — | 声像收窄并收回中央 |

---

### 第三章：Sayuki 引导与测试舱入口

| 说话人 | 具体台词 | 单声道／立体声 | 引擎空间化 | 特殊效果 |
|:---|:---|:---:|:---:|:---|
| **Sayuki** | Hello. I'm a Shadow Patrol Officer. Sayuki. Congratulations on passing the interview. Follow me. | 单声道 | ✓ | — |
| **Player／Hollowone** | The interview? That guy was an interviewer? | 单声道 | ✓ | — |
| **Sayuki** | He's a well-regarded senior member of the Shadow Bureau. They call him Mr. Shadow. He interviewed me, too, back when I first started. Mr. Shadow has a keen eye for people. So, if you got in, it means you've got his seal of approval. | 单声道 | ✓ | — |
| **Player／Hollowone** | Why can't I see anything? | 单声道 | ✓ | — |
| **Sayuki** | Just a minor precaution. The Bureau's interior can't be perceived by outsiders. But you can still see me, right? Just stick close. Vivian. Vivian, I didn't see you there. Nah, it's nothing. I'm just used to taking notes. Hey, don't judge a book by its cover. | 单声道 | ✓ | — |
| **Vivian** | （台词内容无法清晰辨认） | 立体声 | — | **FX-D1** 尖锐失真／破碎粒子化／低可懂度 |
| **Player／Hollowone** | Uh, were you talking about me? | 单声道 | ✓ | — |
| **Sayuki** | She often teases newcomers. Don't worry about it. If your onboarding goes well, you'll prove her wrong. Looks like a meeting's in progress. Wait just a moment. What's this meeting about? Code Red? S.U.N.'s going to have their hands full. Go ahead without me. I need to take this newcomer to the test chamber. Excuse me. Passing through. Excuse me. Sorry. The meeting rooms in this old building are way too small. This place always gets crowded whenever there's a meeting. Um, let's go. | 单声道 | ✓ | — |
| **Player／Hollowone** | Where is the Mind Rot taking place? | 单声道 | ✓ | — |
| **Sayuki** | Oh, in the Upper District. You know how VP is. This kind of thing happens all the time. That's why we're needed. But don't worry about that now. Okay, this is your final test. Give it your all. | 单声道 | ✓ | — |
| **Player／Hollowone** | Another test? | 单声道 | ✓ | — |
| **Sayuki** | Hi, Simmons. Is the test chamber ready? | 单声道 | ✓ | — |
| **Simmons** | DAWN authorization approved. Personnel permitted: two. Preparing the test chamber. Marsha is waiting for you. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩／Simmons 与 Sayuki 共用 |
| **Sayuki（现场）** | I just had my psych evaluation and I'm waiting for the results. So, I'll stay away from the test chamber. I mean, I wouldn't want to disturb Marsha. | 单声道 | ✓ | — |
| **Simmons** | Fine. Seems like replicator number three needs a lens adjustment. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩／Simmons 与 Sayuki 共用 |
| **Sayuki** | Sure. On it. Actually, I could use some help. Would you mind? Go ahead. This will be your last test. | 单声道 | ✓ | — |
| **Simmons** | She won't go easy on you. Good luck. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩／Simmons 与 Sayuki 共用 |

---

### 第四章：Mindbog 思想声与两轮测试

| 说话人 | 具体台词 | 单声道／立体声 | 引擎空间化 | 特殊效果 |
|:---|:---|:---:|:---:|:---|
| **Unknown Voice／Mindbog Thought** | Go to hell! Hideous freak! You're worthless! | 立体声 | — | **FX-D2** 多层叠声／宽化／Doubler 或合唱感 |
| **Sayuki** | Pay no attention to that. They're thoughts from the Mindbog. It powers our test chamber. | 单声道 | ✓ | — |
| **Sayuki（通讯）** | You've got 60 seconds to eliminate the approaching Shadow Monsters. Good luck. Swift and precise. Good job. On to the next one. That was just a basic drill. Fieldwork requires quick action, but remember, speed is secondary to ensuring the safety of civilians. Time for your second trial. Save the civilians without alerting the monsters. Keep a low profile and stay undetected. Use your abilities when needed. Great job. Go through that door and catch your breath. You've earned it. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩／Simmons 与 Sayuki 共用 |

---

### 第五章：测试舱事故与逃生

| 说话人 | 具体台词 | 单声道／立体声 | 引擎空间化 | 特殊效果 |
|:---|:---|:---:|:---:|:---|
| **Player／Hollowone** | What's going on? | 单声道 | ✓ | — |
| **Simmons（通讯）** | The exit's blocked and there's Mind Rot in the chamber. Don't touch it if you want to live. Just opened a new route for you. Up you go. Take the stairs. Run quickly. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Player／Hollowone** | What's the matter? | 单声道 | ✓ | — |
| **Simmons（通讯）** | Mind Rot readings are off the charts. Any trouble downtown? | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Sayuki（通讯）** | Yeah, there's a Code Red in Oakwood District. Can you let the rookie out? | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Simmons（通讯）** | Already on it. I've got more of these bastards to deal with. The exit route is at 60%. Try to keep it together in the meantime. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Sayuki** | That's more than a rookie can handle. | 单声道 | ✓ | — |
| **Simmons（通讯）** | Where are you going? | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Sayuki** | I have to help. | 单声道 | ✓ | — |
| **Simmons（通讯）** | The route's unstable. You'll be trapped inside, too. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Sayuki** | Then make sure to get us out. Hold on, I'm coming. | 单声道 | ✓ | — |
| **Simmons（通讯）** | Damn. The chamber's unstable, but I'll get you out. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Sayuki** | Copy that. I'll clear the monsters to reduce the Mind Rot's interference. Just get that door working. Your power should be more effective against the Jellies. Leave the Suits to me. We'll need to fight till Simmons opens the exit. | 单声道 | ✓ | — |
| **Sayuki（现场）** | Nicely done. We make a good team. Area secured. Looks like the test was wrong about you. You're actually impressive in real combat. Simmons, I'd say we've underestimated this one. | 单声道 | ✓ | — |
| **Simmons（受干扰通讯）** | Exit's almost open. Just hold on. Command invalid. Now, be careful. It's getting closer. | 单声道（中置） | — | **FX-E2** SEAL 通讯处理＋断续／失真／信号干扰 |
| **Sayuki** | Simmons? | 单声道 | ✓ | — |
| **Simmons（受干扰通讯）** | Deploying platforms. | 单声道（中置） | — | **FX-E2** SEAL 通讯处理＋断续／失真／信号干扰 |
| **Sayuki** | Simmons! | 单声道 | ✓ | — |
| **Sayuki（现场／当前操控角色）** | Comms are down. We may be cut off from the outside world. Stay sharp. I've got your back. Falling platforms. Get up there to deploy them. You're a natural. Pull back. Avoid the contaminated zones. HQ must have noticed the anomaly by now. We've got to hold on. | 单声道 | ✓ | — |
| **Player／Hollowone** | What is this thing? | 单声道 | ✓ | — |
| **Sayuki** | This is no ordinary Mind Rot. It's dissolving everything into the Mindbog. | 单声道 | ✓ | — |
| **Mr. Shadow（异常空间声）** | Including you if you stay here. Now, go. | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Simmons（通讯）** | Anyone hurt? | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Sayuki** | I'm fine. Rookie, you okay? | 单声道 | ✓ | — |
| **Player／Hollowone** | I'm okay. | 单声道 | ✓ | — |
| **Simmons（通讯）** | There's a full response underway. Patrol needs you. | 单声道（中置） | — | **FX-E1** 通讯 EQ／明显压缩 |
| **Sayuki** | Be right there. We're wrapping up. You definitely passed the test. Now, I just need to brief you on— | 单声道 | ✓ | — |

---

### 第六章：Mr. Shadow 最终面谈

| 说话人 | 具体台词 | 单声道／立体声 | 引擎空间化 | 特殊效果 |
|:---|:---|:---:|:---:|:---|
| **Mr. Shadow（异常空间声）** | I will take it from here. Hollowone, with me. | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Sayuki** | All right. I appreciate your help. | 单声道 | ✓ | — |
| **Mr. Shadow** | The situation is serious, but they have what it takes. As for you, I'm humbled. Even an entity like me can misjudge your potential. It runs deeper than you realize. But your motivations are not as they appear. Correct? | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Player／Hollowone** | Is this part of the interview? | 单声道 | ✓ | — |
| **Mr. Shadow** | While unofficial, this conversation will determine your future with the Bureau. Why do you want to join SEAL? | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Player／Hollowone** | I'm looking for my killer. | 单声道 | ✓ | — |
| **Mr. Shadow** | Not the most altruistic goal. | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Player／Hollowone** | You're right, but who doesn't have secrets? As long as we serve the Bureau, isn't that enough? | 单声道 | ✓ | — |
| **Mr. Shadow** | A fair point. We share the same goals. You have a way with words. The Bureau needs your help with the Mind Rot incident. Prove yourself worthy of this. | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Player／Hollowone（内心）** | This may be my chance to ask about the killer. | 单声道（中置） | — | — |
| **Player／Hollowone** | Sir, do you happen to know an officer that uses a snake-scale umbrella? | 单声道 | ✓ | — |
| **Mr. Shadow** | Oh? Why the sudden interest? | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Player／Hollowone** | You see, I owe my life to this courageous officer. I want to thank them personally. | 单声道 | ✓ | — |
| **Mr. Shadow** | Expressing gratitude, what a rare trait. I'll help you. Await my message. | 立体声 | — | **FX-C1** 轻微动态立体声／声像持续变化 |
| **Mr. Shadow** | Welcome to SEAL. | 立体声 | — | **FX-C3** 左→右声像移动／空间混响 |

---

### 第七章：调度频道、车内培训与前往外勤

| 说话人 | 具体台词 | 单声道／立体声 | 引擎空间化 | 特殊效果 |
|:---|:---|:---:|:---:|:---|
| **Dispatch Center** | Boyce Park, ready for cleanup. | 单声道（中置） | — | **FX-F1** 车载无线电带宽／通讯 EQ／压缩染色 |
| **Finn（通讯）** | Finn here. On the scene now. | 单声道（中置） | — | **FX-F1** 车载无线电带宽／通讯 EQ／压缩染色 |
| **Dispatch Center** | Requesting additional S.U.N. response in Oakwood. | 单声道（中置） | — | **FX-F1** 车载无线电带宽／通讯 EQ／压缩染色 |
| **Valentina／V（通讯）** | This is V. Be there soon. | 单声道（中置） | — | **FX-F1** 车载无线电带宽／通讯 EQ／压缩染色 |
| **Dispatch Center** | Pruden Hill is expanding. Code Yellow. Looks like someone's already flagged it. | 单声道（中置） | — | **FX-F1** 车载无线电带宽／通讯 EQ／压缩染色 |
| **Sayuki（通讯）** | Unit 08123. Five minutes out. | 单声道 | ✓ | — |
| **Player／Hollowone** | Uh, what exactly is Mind Rot anyway? | 单声道 | ✓ | — |
| **Sayuki** | And this is why proper orientation is so important. Good thing DAWN still has a training tapes feature. | 单声道 | ✓ | — |
| **DAWN（培训模块）** | As you've learned, humanity's collective thoughts manifest as the Rain of Thought. Like water stagnating without proper drainage, it can build up and cause rot. Mind Rot buildups corrode reality, breaking minds, spawning monsters, and warping our world. End of module 14. Proceed to— | 单声道（中置） | — | **FX-G1** DAWN 设备 EQ／档案或磁带式播放染色 |
| **Player／Hollowone** | Huh. Rain of Thought never stops. | 单声道 | ✓ | — |
| **Sayuki** | Nicely put. You're so determined. What made you choose SEAL? | 单声道 | ✓ | — |
| **Player／Hollowone** | An officer changed my life. I joined the force, following his footsteps. Wish I could thank him in person. | 单声道 | ✓ | — |
| **Sayuki** | That explains a lot. | 单声道 | ✓ | — |
| **Player／Hollowone** | I'm hoping my work with everyone gets me closer to finding him. Think you could help with that? | 单声道 | ✓ | — |
| **Sayuki** | We're a team now, so... Okay, but no heroics once we're in the field. If it gets bad, you retreat. Got it? | 单声道 | ✓ | — |
| **Player／Hollowone** | Yes, ma'am. | 单声道 | ✓ | — |
| **Sayuki** | We're here. DAWN has locked down this area. We need to get verified. Technically, you could enter from anywhere, but let's use the main gate this time. Okay. Let's head in. | 单声道 | ✓ | — |

---

### 第八章：DAWN、外勤处置与结尾

| 说话人                      | 具体台词                                                                                                                                                                                                                                                                                      | 单声道／立体声 | 引擎空间化 | 特殊效果                            |
| :----------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-----: | :---: | :------------------------------ |
| **DAWN**                 | Permission updated. Access granted. Hello, Rookie. I'm DAWN, SEAL's companion.                                                                                                                                                                                                            | 单声道（中置） |   —   | **FX-G1** DAWN 设备 EQ／档案或磁带式播放染色 |
| **Sayuki**               | DAWN, are the observation points available?                                                                                                                                                                                                                                               |   单声道   |   ✓   | —                               |
| **DAWN**                 | Yes. Ready to locate nearby monsters. Always a pleasure. Happy to work with everyone's favorite SEAL officer. It looks like that ad campaign is really—                                                                                                                                   | 单声道（中置） |   —   | **FX-G1** DAWN 设备 EQ／档案或磁带式播放染色 |
| **Sayuki**               | Just a few more left. Ready for one last push.                                                                                                                                                                                                                                            |   单声道   |   ✓   | —                               |
| **SEAL HQ（全单位广播）**       | Attention all units. Oakwood has been contained. Emergency status lifted. You may resume regular duties.                                                                                                                                                                                  | 单声道（中置） |   —   | **FX-I1** 全单位优先广播处理             |
| **Sayuki**               | S.U.N. never disappoints. Let's wrap this up and get some coffee. My treat.                                                                                                                                                                                                               |   单声道   |   ✓   | —                               |
| **Dispatch Center（通讯）**  | Pruden Hill contained. Brigade is en route for cleanup. Well done, officers.                                                                                                                                                                                                              | 单声道（中置） |   —   | 窄频／老式电视或广播话筒失真                  |
| **Sayuki（通讯）**           | Roger that. 08123, over.                                                                                                                                                                                                                                                                  |   单声道   |   ✓   | —                               |
| **Dispatch Center（通讯）**  | Well done, officers.                                                                                                                                                                                                                                                                      | 单声道（中置） |   —   | 窄频／老式电视或广播话筒失真                  |
| **Sayuki**               | Oh, almost forgot. Your reward for your first assignment. Shock Americano. Perfect for staying alert, fighting off fatigue, and doing your best. All that Mind Rot cleared, and we're still buried in work back at SEAL. Well, Director Nian has big plans, but they're hard to pull off. |   单声道   |   ✓   | —                               |
| **Player／Hollowone**     | He seems a bit unreliable.                                                                                                                                                                                                                                                                |   单声道   |   ✓   | —                               |
| **Sayuki**               | Then introduce me to more reliable people like you.                                                                                                                                                                                                                                       |   单声道   |   ✓   | —                               |
| **Player／Hollowone**     | I'll ask around online.                                                                                                                                                                                                                                                                   |   单声道   |   ✓   | —                               |
| **Sayuki**               | Great. Can't wait to interview them in person.                                                                                                                                                                                                                                            |   单声道   |   ✓   | —                               |
| **Player／Hollowone**     | By the way, what was the director's big plan?                                                                                                                                                                                                                                             |   单声道   |   ✓   | —                               |
| **Sayuki**               | To save the world.                                                                                                                                                                                                                                                                        |   单声道   |   ✓   | —                               |
| **Unknown Vocalization** | Ooh. Ooh.                                                                                                                                                                                                                                                                                 |   立体声   |   —   | 片尾人声化处理                         |