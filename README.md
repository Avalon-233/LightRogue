# LightRogue · 光照肉鸽

一款基于 **C++ + SFML 3.x** 的 2D Roguelike 生存游戏，灵感来源于 *Vampire Survivors*。玩家在黑暗中探索，利用光照系统对抗不断涌来的敌人，存活尽可能长的时间。

> 📘 **课程项目说明**
>
> 本项目为厦门大学本科生《程序设计实验》课程的大作业，由 **3 人小组** 在 **3 周** 内合作完成。受限于时间与经验，代码结构、美术资源与游戏平衡性均较为粗糙，仅作学习交流之用，欢迎提出建议与指正。

## 🎮 游戏特色

- **光照系统** — 玩家自带光源，视野受限于光照范围，不可见区域被战争迷雾覆盖
- **多种敌人** — 4 种敌人类型：
  - 🟢 **Basic** — 基础追击型
  - 🔵 **Ranged** — 远程射击型
  - 🔴 **Bomber** — 自爆型
  - 🟣 **Giant** — 大型精英怪（6 分钟后出现）
- **成长系统** — 拾取经验光球升级，每次升级可选择强化方向
- **音效与 BGM** — 完整的音效反馈（射击、受伤、升级等）
- **存档系统** — 支持进度保存与读取
- **生存模式** — 单局 6 分钟，敌人随时间增多增强

## 🛠️ 技术栈

| 项目 | 说明 |
|------|------|
| 语言 | C++ |
| 图形库 | SFML 3.1.0 |
| 构建工具 | Visual Studio 2022 (MSVC) |
| 分辨率 | 1440×810 固定 View + Letterbox |

## 📁 项目结构

```
program/
├── LightRogue/          # 游戏源码 (VS 项目主体)
│   ├── Game.cpp/h       # 主循环、事件处理、状态机
│   ├── GameWorld.cpp/h  # 对象管理、碰撞、生成、光照
│   ├── Player.cpp/h     # 玩家控制、攻击、光照能量
│   ├── Enemy.cpp/h      # 敌人 AI (4 种类型)
│   ├── Projectile.cpp/h # 子弹 (玩家/敌人)
│   ├── Pickup.cpp/h     # 掉落物 (经验/血量)
│   ├── UI.cpp/h         # UI 系统 (血条、经验条、升级面板)
│   ├── SoundManager.cpp/h  # 音效管理
│   ├── SaveManager.cpp/h   # 存档读写
│   ├── ResourceLoader.h        # 资源加载
│   └── SFML-3.1.0/            # SFML 库文件
├── resource/            # 游戏资源
│   ├── *.png            # 精灵图 (玩家、敌人、子弹、拾取物)
│   ├── *.wav            # 音效
│   ├── BGM.ogg          # 背景音乐
│   └── background.png   # 地图背景
├── docs/                # 设计文档
│   └── class_design.md  # 类关系图 (Mermaid)
├── tests/               # 测试
└── README.md
```

## 🏗️ 架构设计

```
Game (主循环 + 状态机)
 └── GameWorld (对象管理 + 碰撞 + 生成 + 光照)
      ├── Player        — 玩家控制、光照能量
      ├── Enemy[]       — 敌人 AI、分波次生成
      ├── Projectile[]  — 子弹
      ├── Pickup[]      — 掉落物
      ├── UIManager     — HUD、升级面板、菜单
      ├── SoundManager  — 音效播放
      └── SaveManager   — 存档系统
```

核心采用 `unique_ptr` 管理游戏对象，`GameWorld` 统一负责更新、碰撞和渲染。

## 🚀 构建与运行

### 环境要求

- Windows 10/11
- Visual Studio 2022（需安装 C++ 桌面开发工作负载）
- SFML 3.1.0（已包含在 `LightRogue/SFML-3.1.0/`）

### 步骤

1. 用 Visual Studio 打开 `LightRogue/LightRogue.slnx`
2. 选择 **x64 + Release** 配置
3. 生成解决方案 (`Ctrl+Shift+B`)
4. 将 `resource/` 文件夹复制到可执行文件所在目录
5. 运行游戏

## 🎯 操作

| 按键 | 功能 |
|------|------|
| WASD / 方向键 | 移动 |
| 鼠标左键 | 攻击 |
| Esc | 暂停 |

## 📝 备注

- 编译产物 (`*.exe`, `*.obj`, `*.pdb` 等) 已通过 `.gitignore` 排除
- 资源文件较大，如需减小仓库体积可考虑使用 Git LFS
