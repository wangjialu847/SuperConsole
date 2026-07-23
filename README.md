# 🎮 SuperConsole

**按 Insert 键，游戏就是你的。**

一个运行在 Unity Mono 游戏内部的高权限运行时修改工具 / 模组制作平台。

> 普通修改器给你 100 个功能，你只能用 100 个。
>
> SuperConsole 给你**创造功能**的能力，功能没有上限。

---

## 📖 目录

- [快速开始](#-快速开始)
- [安装方法](#-安装方法)
- [快捷键大全](#-快捷键大全)
- [核心功能详解](#-核心功能详解)
- [逻辑体V2 模组系统](#-逻辑体v2-模组系统)
- [DLL 扩展开发](#-dll-扩展开发)
- [编译项目](#-编译项目)
- [目录结构](#-目录结构)
- [常见问题](#-常见问题)
- [开源协议](#-开源协议)

---

## 🚀 快速开始

### 安装

1. 安装 **BepInEx** 到游戏目录
2. 把 **SuperConsole.dll** 放到 `BepInEx/plugins/`
3. 启动游戏
4. 按 **Insert** 键召唤控制台
5. 开始为所欲为！

### 第一个操作

1. 按 `Insert` 打开控制台
2. 点击「对象浏览器」
3. 在左侧找一个对象（比如 `Player`）
4. 点击选中，右侧显示它的组件
5. 展开组件，找到 `health` 字段
6. 修改数值，点击「设置」
7. 游戏里的血量就变了！

---

## 📦 安装方法

### 前置要求

| 要求 | 说明 |
|------|------|
| 游戏类型 | Unity Mono（**不是** Il2Cpp） |
| 插件框架 | BepInEx 5.x |
| 系统 | Windows / macOS / Linux |

### 安装步骤

**1. 下载 BepInEx**

```
https://github.com/BepInEx/BepInEx/releases
```

解压到游戏根目录

**2. 下载 SuperConsole**

从 Releases 页面下载 `SuperConsole.dll`

**3. 放置文件**

```
SuperConsole.dll → BepInEx/plugins/
```

**4. 启动游戏**

控制台出现 BepInEx 日志即为成功

**5. 按 Insert**

召唤 SuperConsole 主界面

### 验证安装

启动游戏后，BepInEx 控制台应显示：

```
[SuperConsole] 超级控制台已加载！按 Insert 键召唤。
[SuperConsole] 按 Home 键打开 Hook 管理器 | 按 End 键打开方法管理器
[SuperConsole] 对象浏览器 + 左键 选择物体 | 自由视角: 按 F 切换
[LogicManagerV2] ✅ 初始化完成，找到 0 个逻辑体
```

---

## 🎮 快捷键大全

| 按键 | 功能 | 说明 |
|------|------|------|
| `Insert` | 打开/关闭主控制台 | 核心入口 |
| `Home` | 打开 Hook 管理器 | 管理所有 Hook |
| `End` | 打开方法管理器 | 扫描/搜索/执行方法 |
| `F` | 切换自由视角 | 控制台关闭时有效 |
| `Ctrl + 左键` | 选中物体 | 在对象浏览器打开时点击游戏物体 |
| `N` | 重置所有窗口位置 | 窗口跑出屏幕时使用 |
| `PageUp` | 打开帮助中心 | 内置完整文档 |
| `Esc` | 关闭当前窗口 | 退出自由视角/关闭窗口 |
| `Enter` | 执行代码 | 在控制台输入框中 |

---

## ⚡ 核心功能详解

### 🔍 内存搜索

**Cheat Engine** 级别的内存搜索工具。

#### 搜索模式（11种）

| 模式 | 说明 |
|------|------|
| 精确 | 搜索精确数值 |
| 大于 | 搜索大于指定值的数值 |
| 小于 | 搜索小于指定值的数值 |
| 大于等于 | 搜索大于等于指定值的数值 |
| 小于等于 | 搜索小于等于指定值的数值 |
| 范围 | 搜索在 min-max 之间的数值 |
| 变化 | 搜索值发生变化的字段 |
| 不变 | 搜索值未发生变化的字段 |
| 增加 | 搜索值增加的字段 |
| 减少 | 搜索值减少的字段 |
| 模糊 | 近似匹配（容差 10%） |

#### 数据类型（9种）

`自动`、`float`、`int`、`double`、`long`、`short`、`byte`、`bool`、`string`

#### 使用步骤

1. 打开控制台 → 点击「内存搜索」
2. 选择搜索模式（默认：精确）
3. 选择数据类型（默认：自动）
4. 输入搜索值
5. 点击「搜索」
6. 在结果列表中点击「选择」锁定目标
7. 在「修改为」输入框输入新值
8. 点击「修改选中」或「修改所有」
9. 点击「锁定选中」可锁定数值（每帧自动恢复）

#### 进阶技巧：多步搜索法

1. 第一次搜索：精确 → 找到一批结果
2. 在游戏中改变目标值（如扣血/加钱）
3. 切换到 SuperConsole
4. 选择「变化」模式 → 点击「过滤」
5. 重复几次 → 精确定位到目标值

---

### 🔍 对象浏览器

查看和修改场景中所有对象的工具。

#### 功能列表

| 功能 | 说明 |
|------|------|
| 树形层级 | 显示场景中所有对象的父子关系 |
| 对象搜索 | 按名称搜索对象 |
| 组件列表 | 显示对象上的所有组件 |
| 组件展开 | 查看组件的所有字段（包括私有） |
| 字段编辑 | 修改 float/int/bool 类型的字段值 |
| 组件启用/禁用 | 切换组件状态 |
| 组件添加/删除 | 添加或删除组件（**带自动补全！**） |
| 对象锁定 | 锁定对象所有数值字段 |
| 骨骼查看 | 一键打开骨骼浏览器 |
| 碰撞箱查看 | 显示/高亮碰撞箱 |
| 传送功能 | 传送玩家到对象位置 |

#### 选中物体方式

- **方式1**：在对象浏览器左侧树形列表中点击
- **方式2**：打开对象浏览器后，在游戏场景中 `左键` 点击物体

#### 添加组件（带自动补全）

在「添加组件」输入框中输入组件名，会自动弹出补全列表：

- 按 `↑` `↓` 选择
- 按 `Enter` 确认
- 按 `Esc` 取消

---

### 🦴 骨骼系统

包含三个骨骼相关工具，从查看、编辑到动画，全套搞定。

#### 骨骼浏览器 (BoneVisualizer)

查看角色骨架结构。

**使用方法：**

1. 在对象浏览器中选中一个对象
2. 点击「骨骼」按钮
3. 树形显示所有骨骼
4. 点击骨骼名称 → 高亮显示
5. 5 种颜色可切换：蓝 红 绿 黄 紫

**显示选项：**

| 选项 | 说明 |
|------|------|
| Skeleton | 显示骨骼连线 |
| Outline | 显示包围盒 |
| Names | 显示骨骼名称 |

#### 骨骼姿势编辑器 (BonePoseEditor)

实时调整骨骼位置/旋转/缩放。

**使用方法：**

1. 在对象浏览器中选中一个对象
2. 点击「姿势编辑」按钮
3. 在骨骼列表中选择要编辑的骨骼
4. 切换编辑模式：
   - 位置 - 修改 `localPosition`
   - 旋转 - 修改 `localRotation`
   - 缩放 - 修改 `localScale`
5. 输入数值 → 点击「应用」

**批量操作：**

| 操作 | 说明 |
|------|------|
| 批量偏移位置 | 所有骨骼偏移指定值 |
| 批量偏移旋转 | 所有骨骼偏移指定角度 |
| 统一缩放 | 所有骨骼统一缩放 |
| 重置所有骨骼 | 恢复所有骨骼到零点 |
| X轴镜像 | 自动镜像左右对称骨骼 |

**姿势管理：**

1. 调整好骨骼姿态后，输入姿势名称
2. 点击「保存姿势」→ 保存当前姿态
3. 点击「加载姿势」→ 恢复之前保存的姿态

#### 骨骼动画扩展 (BoneAnimationExtension)

让角色播放骨骼动画。

**内置动画：**

| 动画名 | 效果 |
|--------|------|
| idle | 呼吸浮动 |
| walk | 腿部交替摆动 + 身体起伏 |
| jump | 跳跃弧线 + 手臂上摆 |
| wave | 挥手 |
| dance | 扭动 |
| float | 漂浮 |
| spin | 旋转 |
| bounce | 弹跳 |

**使用方式：**

**方式1：逻辑体动作**

在逻辑体编辑器中添加动作：
- 动作类型: `PlayBoneAnim`
- 目标: `对象名.动画名`
- 例: `Player.idle`

**方式2：控制台命令**

```
boneanim Player idle
```

**方式3：代码调用**

```csharp
BoneAnimationExtension.PlayAnimation("Player", "dance");
```

---

### 🔗 Hook 管理器

拦截游戏方法执行，修改游戏行为。按 `Home` 键打开。

#### 6 个预设 Hook

| Hook | 拦截的方法 | 效果 |
|------|-----------|------|
| 禁用晕倒 | `RagdollController.Knockout` | 玩家不会晕倒 |
| 禁用伤害 | `PlayerCharacter.TakeDamage` | 玩家免疫伤害 |
| 禁用死亡 | `PlayerCharacter.Die` | 玩家不会死亡 |
| 禁用扣血 | `PlayerCharacter.ApplyDamage` | 阻止扣血 |
| 禁用重力 | `Rigidbody.UpdateGravity` | 玩家浮在空中 |
| 禁用物理 | `Physics.Simulate` | 冻结物理世界 |

#### 自定义 Hook

在 `extensions/` 中创建 DLL，实现 `IHookPreset` 接口即可。

---

### 🔧 方法管理器

扫描、搜索、执行、拦截游戏中的方法。按 `End` 键打开。

| 功能 | 说明 |
|------|------|
| 方法列表 | 显示预设的常用方法 |
| 搜索方法 | 按类型名/方法名搜索 |
| 执行方法 | 执行 public/private 方法 |
| 拦截方法 | 阻止方法执行 |

---

### 🔒 对象锁定系统

锁定数值，每帧自动恢复，**重生/读档/重启都有效**。

**使用方法：**

1. 在对象浏览器中选中一个对象
2. 点击「锁定此对象」→ 锁定所有数值字段
3. 点击「解锁此对象」解除锁定

**或者用代码：**

```csharp
ObjectLocker.Lock("对象名", "组件名", "字段名", 值);
ObjectLocker.Unlock("对象名", "组件名", "字段名");
```

---

### 📍 传送系统

两种传送模式。

**坐标模式：**

1. 在对象浏览器中选中要传送的对象
2. 点击「传送」按钮
3. 输入 X/Y/Z 坐标
4. 点击「传送到坐标」

**物体模式：**

1. 点击「点击选择物体」
2. 在游戏场景中点击一个目标物体
3. 自动返回窗口确认
4. 点击「传送到物体」

---

### 🎨 资源提取器

从游戏中提取资源。

**支持提取的类型：**

| 类型 | 格式 | 说明 |
|------|------|------|
| 纹理 (Texture2D) | `.png` | 保存为 PNG |
| 模型 (Mesh) | `.obj` | 保存为 OBJ |
| 音频 (AudioClip) | `.wav` | 记录引用 |
| 材质 (Material) | `.mat` | 保存材质属性 |
| 动画 (AnimationClip) | `.anim` | 保存动画数据 |

**使用方法：**

1. 打开控制台 → 点击「资源提取」
2. 点击「刷新」扫描当前场景
3. 按类型筛选：全部/纹理/模型/音频/材质/动画
4. 搜索资源名称
5. 点击「提取」保存资源
6. 点击「定位」在场景中高亮资源所属对象

---

### 📝 C# 代码执行

直接在控制台执行任意 C# 代码。

**示例：**

```csharp
// 改血量
GameObject.Find("PlayerCharacter(Clone)").GetComponent<PlayerCharacter>().health = 9999;

// 找对象
GameObject.Find("PlayerCharacter(Clone)");

// 修改速度
GameObject.Find("PlayerCharacter(Clone)").GetComponent<PlayerCharacterMovement>().speedMultiplier = 999f;

// 游戏速度
Time.timeScale = 5f;

// 遍历所有玩家
PlayerCharacter[] players = FindObjectsOfType<PlayerCharacter>();
foreach (var p in players) { p.health = 9999; }

// 锁定数值
ObjectLocker.Lock("PlayerCharacter(Clone)", "PlayerCharacter", "health", 9999);

// 查看锁定状态
ObjectLocker.GetStatus();
```

**命令字典：** 点击「字典」按钮，有 18 个常用代码模板，一键填入输入框。

---

## 🧠 逻辑体V2 模组系统

逻辑体 V2 是 SuperConsole 的**模组系统**。把一个游戏对象变成**可导出、可分享、可复用**的模组。

### 文件结构

```
Logics/我的角色/
├── mod.json                      ← 识别文件 + 元数据
├── prefabs/
│   └── main.prefab               ← 预制体（二进制+文本双格式）
├── models/
│   └── character.obj             ← 模型
├── textures/
│   └── diffuse.png               ← 纹理
├── materials/
│   └── character.mat             ← 材质
├── animations/
│   └── idle.anim                 ← 动画
└── logic.dll                     ← 对象专属 DLL（可选）
```

### mod.json 格式

```json
{
  "id": "a1b2c3d4e5",
  "name": "我的角色",
  "version": "1.0.0",
  "author": "玩家",
  "description": "从游戏提取的角色",
  "type": "Character",
  "enabled": true,
  "resources": {
    "Prefab": "prefabs/main.prefab",
    "Model": "models/character.obj",
    "Textures": ["textures/diffuse.png"],
    "Audio": [],
    "Materials": ["materials/character.mat"],
    "Animations": [],
    "Scripts": [],
    "DLL": "logic.dll"
  },
  "dependencies": [],
  "tags": ["角色", "提取"]
}
```

### 支持的类型

| 类型 | 说明 |
|------|------|
| Prefab | 单个预制体 |
| Scene | 完整场景 |
| Map | 地图/关卡 |
| Character | 角色 |
| Weapon | 武器 |
| Vehicle | 载具 |
| Prop | 道具/装饰 |
| Mod | 完整模组（包含多种资源） |

### 提取流程

**从游戏对象提取：**

1. 在对象浏览器中选中一个对象
2. 打开控制台 → 点击「逻辑体」
3. 点击「提取当前对象」
4. 自动提取：
   - `Mesh` → `models/xxx.obj`
   - `Texture` → `textures/xxx.png`
   - `Material` → `materials/xxx.mat`
   - `Animation` → `animations/xxx.anim`
   - 层级结构 → `prefabs/main.prefab`
5. 保存到 `Logics/` 目录

**从场景提取：**

1. 打开控制台 → 点击「逻辑体」
2. 点击「提取场景」
3. 自动扫描场景所有对象
4. 提取所有资源
5. 保存为 `Scene` 类型的逻辑体

### 召唤流程

1. 打开控制台 → 点击「逻辑体」
2. 在列表中选择一个逻辑体
3. 点击「召唤到玩家」或「召唤到鼠标」
4. 自动加载资源：
   - 读取 `mod.json` → 获取资源列表
   - 加载预制体（`.prefab`）
   - 加载模型（`.obj` → `Mesh`）
   - 加载纹理（`.png` → `Texture2D`）
   - 加载材质（`.mat` → `Material`）
   - 加载动画（`.anim` → `AnimationClip`）
   - 加载 DLL（`logic.dll` → 附加组件 + 初始化）
5. 对象出现在场景中！

### 批量召唤

1. 选中一个逻辑体
2. 点击「批量召唤」
3. 在当前位置生成 5 个（随机分布）

### 分享模组

**导出：**

1. 选中一个逻辑体
2. 点击「导出 .mod」
3. 在 `Logics/` 目录生成 `.mod` 文件
4. 分享给朋友

**导入：**

1. 把 `.mod` 文件放到 `Logics/` 目录
2. 点击「导入 .mod」
3. 自动解压到同名文件夹
4. 刷新列表，即可召唤

### 3D 预览

1. 选中一个逻辑体
2. 点击「3D 预览」
3. 在预览窗口中：
   - 拖拽旋转视角
   - 滚轮缩放
   - 显示/隐藏 模型/骨骼/碰撞箱/网格/轴
   - 选择骨骼 → 实时编辑位置/旋转/缩放
   - 碰撞箱列表 → 查看/编辑/删除
   - 保存修改 → 应用到对象

这几乎就是一个**迷你 Unity Editor**！

### 逻辑体 DLL 扩展

为逻辑体编写专属 DLL，实现 `ILogicObject` 接口：

```csharp
using SuperConsole;
using UnityEngine;

public class MyLogic : ILogicObject
{
    private GameObject obj;
    private float health = 100f;

    public void OnSpawn(GameObject gameObject, LogicEntityV2 logic)
    {
        obj = gameObject;
        Debug.Log($"逻辑体 {logic.name} 已召唤！");
    }

    public void OnUpdate()
    {
        // 每帧更新逻辑
        if (health <= 0)
        {
            Object.Destroy(obj);
        }
    }

    public void OnDestroy(GameObject gameObject)
    {
        Debug.Log("逻辑体被销毁了！");
    }

    public void OnMessage(string message, object data)
    {
        if (message == "TakeDamage")
        {
            health -= (float)data;
        }
    }
}
```

**编译并放置：**

1. 编译为 `logic.dll`
2. 放到逻辑体文件夹（与 `mod.json` 同级）
3. 在 `mod.json` 中设置 `"DLL": "logic.dll"`
4. 召唤逻辑体时自动加载

---

## 🔌 DLL 扩展开发

SuperConsole 拥有**两套 DLL 系统**，各司其职：

### 两套 DLL 系统对比

| | 全局扩展 DLL | 逻辑体 DLL |
|--|-------------|-----------|
| 位置 | `extensions/*.dll` | `Logics/某逻辑体/logic.dll` |
| 加载者 | `ExtensionLoader` | `LogicDLLLoader` |
| 加载时机 | 游戏启动时 | 召唤逻辑体时 |
| 生命周期 | 全局（游戏全程） | 跟随逻辑体（生成→销毁） |
| 管什么 | SuperConsole 本身 + 游戏全局 | 这一个逻辑体对象 |
| 范围 | 整个游戏 | 一个对象 |
| 接口 | `IExtensionInit` / `IUniversalExtension` | `ILogicObject` / `ILogicComponent` |

### 全局扩展 DLL 能做什么

放在 `extensions/` 目录，管整个游戏和 SuperConsole 本身：

| 类别 | 能做什么 | 示例 |
|------|---------|------|
| 命令 | 注册控制台命令 | `cmd:mycommand` |
| 窗口 | 创建自定义 UI 窗口 | 自己的工具面板 |
| Hook | 拦截游戏方法 | 禁用伤害、改重力 |
| 逻辑体 | 注册逻辑体类型 | 新类型 `Weapon` |
| 脚本 | 注册可执行脚本 | 自动执行任务 |
| 预制体 | 提供预制体 | 给逻辑体用 |
| 资源 | 加载/管理资源 | 模型、贴图、音频 |
| 网络 | HTTP/WebSocket | 下载模组、联机 |
| 文件 | 读写文件 | 配置、存档、日志 |
| 游戏 | 修改游戏全局 | 时间、物理、场景 |
| UI | 修改/添加游戏UI | 改颜色、加按钮 |
| 其他 | 任何你能想到的 | AI、自动化、数据分析 |

### 逻辑体 DLL 能做什么

放在 `Logics/某逻辑体/logic.dll`，管这一个对象：

| 类别 | 能做什么 | 示例 |
|------|---------|------|
| 对象控制 | 控制这个对象的行为 | AI、移动、攻击 |
| 生命周期 | 生成/销毁回调 | `OnSpawn`、`OnDestroy` |
| 每帧更新 | 每帧执行逻辑 | `OnUpdate` |
| 消息通信 | 接收/发送消息 | `OnMessage` |
| 组件挂载 | 挂载自定义组件 | 附加 MonoBehaviour |
| 游戏交互 | 和游戏交互 | 打人、捡东西、对话 |
| 数据管理 | 管理自己的数据 | 血量、状态、位置 |
| 资源访问 | 访问自己的资源 | 自己的模型/贴图 |

### 全局扩展 — 7 种接口

| 接口 | 用途 |
|------|------|
| `IExtensionInit` | 加载/卸载回调（必须实现） |
| `IUniversalExtension` | 万能接口（**推荐**） |
| `ICommand` | 注册控制台命令 |
| `IWindow` | 创建自定义窗口 |
| `IHookPreset` | 注册 Hook 预设 |
| `ILogicEntity` | 注册逻辑体 |
| `IPrefabProvider` | 提供预制体 |

### 最小全局扩展（5 行代码）

```csharp
using SuperConsole;
using UnityEngine;

public class MyExtension : IExtensionInit
{
    public void OnLoad() { Debug.Log("扩展加载了！"); }
    public void OnUnload() { Debug.Log("扩展卸载了！"); }
}
```

### 完整全局扩展（推荐方式）

```csharp
using System;
using UnityEngine;
using SuperConsole;

public class MyMod : IUniversalExtension
{
    public void OnLoad(ExtensionContext ctx)
    {
        ctx.Log("我的扩展加载了！");

        // 1. 注册命令
        ctx.RegisterCommand("mycmd", (args) => {
            ctx.Log("执行了 mycmd！参数: " + string.Join(", ", args));
        });

        // 2. 注册窗口
        ctx.RegisterWindow("我的工具", () => {
            GUILayout.Label("这是我的工具窗口！");
            if (GUILayout.Button("改血量")) {
                var player = GameObject.Find("PlayerCharacter(Clone)");
                if (player != null) {
                    var pc = player.GetComponent<PlayerCharacter>();
                    if (pc != null) pc.health = 9999;
                }
            }
        });

        // 3. 注册 Hook
        ExtensionCommands.RegisterHook(
            "PlayerCharacter",
            "TakeDamage",
            before: () => { ctx.Log("即将受到伤害！"); },
            after: () => { ctx.Log("伤害已应用！"); }
        );

        // 4. 执行代码
        ctx.ExecuteCode("Debug.Log('动态执行代码！');");
    }

    public void OnUnload()
    {
        Debug.Log("扩展卸载了！");
    }
}
```

### ExtensionContext 提供的工具

| 方法 | 说明 |
|------|------|
| `RegisterCommand(name, action)` | 注册控制台命令 |
| `RegisterWindow(title, drawAction)` | 注册自定义窗口 |
| `Log(msg)` / `LogWarning(msg)` / `LogError(msg)` | 输出日志 |
| `Output(msg)` | 向 SuperConsole UI 输出消息 |
| `ExecuteCode(code)` | 执行 C# 代码 |

### 各接口详细示例

**使用 ICommand 接口**

```csharp
public class MyCommand : ICommand
{
    public string Name => "hello";
    public string Code => "hello <名字>";
    public string Description => "打招呼";
}
```

**使用 IWindow 接口**

```csharp
public class MyWindow : IWindow
{
    public string Title => "我的面板";

    public void Draw()
    {
        GUILayout.Label("这是我的面板！");
        if (GUILayout.Button("点击我")) {
            Debug.Log("被点击了！");
        }
    }
}
```

**使用 IHookPreset 接口**

```csharp
public class MyHook : IHookPreset
{
    public string DisplayName => "禁用伤害";
    public string TypeName => "PlayerCharacter";
    public string MethodName => "TakeDamage";
    public string Description => "让玩家免疫伤害";
    public string HookType => "Prefix";

    public bool Prefix()
    {
        return false; // false = 阻止原方法执行
    }
}
```

**使用 ILogicEntity 接口**

```csharp
public class AutoHeal : ILogicEntity
{
    public string Name => "自动回血";
    public string Description => "血量低于50%自动回血";

    public void Execute()
    {
        var player = GameObject.Find("Player");
        var health = player.GetComponent<PlayerCharacter>().health;
        if (health < 50) {
            player.GetComponent<PlayerCharacter>().health = 100;
        }
    }
}
```

**使用 IPrefabProvider 接口**

```csharp
public class MyPrefab : IPrefabProvider
{
    public string Name => "魔法剑";

    public GameObject GetPrefab()
    {
        return Resources.Load<GameObject>("Sword");
    }
}
```

### 编译扩展

```
csc /target:library /r:SuperConsole.dll /r:UnityEngine.CoreModule.dll MyExtension.cs
```

### 部署扩展

1. 编译得到 `MyExtension.dll`
2. 放到 `BepInEx/plugins/SuperConsole/extensions/`
3. 启动游戏（或输入 `ext reload`）
4. 扩展自动加载！

### 管理扩展

| 命令 | 说明 |
|------|------|
| `ext list` | 列出所有扩展 |
| `ext reload` | 重新加载所有扩展 |
| `ext disable xxx.dll` | 禁用指定扩展 |
| `ext enable xxx.dll` | 启用指定扩展 |

---

## 🛠️ 编译项目

### 需要的 DLL

| DLL | 来源 |
|-----|------|
| `UnityEngine.CoreModule.dll` | 游戏目录/Managed/ |
| `UnityEngine.IMGUIModule.dll` | 游戏目录/Managed/ |
| `UnityEngine.UI.dll` | 游戏目录/Managed/ |
| `BepInEx.dll` | BepInEx/core/ |
| `0Harmony.dll` | BepInEx/core/ |
| `Microsoft.CodeAnalysis.dll` | NuGet |
| `Microsoft.CodeAnalysis.CSharp.dll` | NuGet |
| `System.Collections.Immutable.dll` | NuGet |
| `System.Reflection.Metadata.dll` | NuGet |

### 命令行编译

```
csc /target:library /r:"依赖库/*.dll" SuperConsole.cs
```

### Visual Studio 编译

打开 `SuperConsole.csproj` 即可编译。

---

## 📂 目录结构

```
SuperConsole/
├── SuperConsole.dll              # 主插件
├── extensions/                   # 全局扩展 DLL
│   └── Disabled/                 # 已禁用的扩展
├── Assets/                       # 本地资源
│   ├── Models/                   # 模型 (.obj, .fbx)
│   ├── Textures/                 # 贴图 (.png, .jpg)
│   ├── Audio/                    # 音频 (.wav, .mp3)
│   ├── Prefabs/                  # 预制体 (.prefab)
│   ├── Animations/               # 动画 (.anim)
│   └── Materials/                # 材质 (.mat)
├── Logics/                       # 逻辑体模组
│   └── (每个逻辑体一个文件夹)
│       ├── mod.json
│       ├── prefabs/
│       ├── models/
│       ├── textures/
│       ├── materials/
│       ├── animations/
│       └── logic.dll             # 逻辑体专属 DLL
├── scripts/                      # C# 脚本
├── Hooks/                        # Hook 配置
└── config/                       # 配置文件
```

---

## ❓ 常见问题

**Q：SuperConsole 是什么？**

A：一个运行在 Unity Mono 游戏内部的高权限运行时修改工具。按 Insert 键召唤，然后想干什么就干什么。

---

**Q：全局扩展 DLL 和逻辑体 DLL 有什么区别？**

| | 全局扩展 DLL | 逻辑体 DLL |
|--|-------------|-----------|
| 位置 | `extensions/` | `Logics/某逻辑体/` |
| 管什么 | 整个游戏 + SuperConsole | 这一个对象 |
| 加载时机 | 游戏启动 | 召唤逻辑体时 |
| 生命周期 | 游戏全程 | 跟随对象 |

---

**Q：骨骼浏览器、姿势编辑器、动画扩展有什么区别？**

| 工具 | 用途 | 作用 |
|------|------|------|
| 骨骼浏览器 | 查看 | 显示骨架树形结构 |
| 姿势编辑器 | 编辑 | 修改位置/旋转/缩放 |
| 动画扩展 | 播放 | 播放预设动画 |

---

**Q：逻辑体 V1 和 V2 有什么区别？**

| 功能 | V1 | V2 |
|------|----|----|
| 条件-动作编辑 | ✅ | ❌（用代码代替） |
| 预制体提取 | ❌ | ✅ |
| 资源导出 | ❌ | ✅ (.obj/.png/.mat/.anim) |
| 模组分享 | ❌ | ✅ (.mod 打包) |
| 3D 预览 | ❌ | ✅ |
| DLL 支持 | ❌ | ✅ |
| 场景提取 | ❌ | ✅ |

---

**Q：这玩意儿权限高吗？**

A：高到离谱。运行在游戏进程内部，可以：

- 读取/修改任何内存
- 拦截/修改任何方法
- 执行任意 C# 代码
- 加载任意 DLL
- 创建/删除任何对象
- 提取任何资源

唯一限制：必须装 BepInEx。

---

**Q：会封号吗？**

A：如果有反作弊（EAC/BattlEye），可能会被检测。建议只在单机游戏或私人服务器使用。

你用来干什么，我不负责。MIT 协议，出了事别找我。

---

**Q：能支持 Il2Cpp 吗？**

A：目前只支持 Mono。Il2Cpp 需要重写，等未来吧（可能不会）。

---

**Q：我能做什么？**

A：你可以：

- 改游戏参数（血量/速度/金钱）
- 提取游戏资源（模型/纹理/音频）
- 编辑骨骼姿势（给角色摆 Pose）
- 播放骨骼动画（让角色动起来）
- 写全局扩展 DLL（加命令/加窗口/加 Hook）
- 写逻辑体 DLL（控制对象行为）
- 写逻辑体模组（导出/分享）

一切取决于你的想象力。

---

**Q：遇到问题怎么办？**

1. 检查 BepInEx 是否正确安装
2. 检查 SuperConsole.dll 是否在 `plugins/`
3. 检查游戏是否为 Unity Mono（不是 Il2Cpp）
4. 查看日志（`BepInEx/LogOutput.log`）
5. 我不管了，你自己修（MIT）

---

## 📄 开源协议

MIT License

你可以：

- ✅ 商业使用
- ✅ 修改代码
- ✅ 分发代码
- ✅ 私人使用

你只需要：

- 📌 保留版权声明

---

## 🙏 致谢

- **BepInEx** - Unity 插件框架
- **Harmony** - 运行时补丁库
- **Roslyn** - C# 编译器

---

## ⭐ Star 支持

如果这个项目帮到了你，点个 Star 支持一下吧！

---

**按 Insert，开始你的游戏改造之旅。** 🚀
