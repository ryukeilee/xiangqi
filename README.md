# 中国象棋 / Chinese Chess (Xiangqi)

> 单文件 · 零依赖 · 双击即玩 | Single-file · Zero dependencies · Double-click to play

[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Size](https://img.shields.io/badge/size-27KB-green)](index.html)
[![Platform](https://img.shields.io/badge/platform-browser-orange)]()

---

## 中文

### 项目简介

中国象棋（ Xiangqi ）是一款完全离线的单文件 HTML 棋类游戏。无需安装、无需服务器、无需网络 — 下载 `index.html`，双击即可在浏览器中打开。

内置完整规则引擎、三档难度 AI、棋谱记录，支持人人对战和人机对战两种模式。

### 快速开始

```bash
git clone https://github.com/ryukeilee/xiangqi.git
cd xiangqi
open index.html     # macOS
# 或直接双击 index.html（Windows / Linux）
```

或者直接下载 [index.html](index.html)，双击打开。

### 功能特性

**🎮 游戏模式**

| 模式 | 说明 |
|------|------|
| 人人对战 | 同一设备双人轮流落子 |
| 人机对战 | 内置 AI，三档难度可选 |

**♟️ 规则引擎**

- 全部 7 种棋子合法走法校验：
  - 将/帅 — 九宫内一步直行，飞将（将帅对面）检测
  - 仕/士 — 九宫内一步斜行
  - 相/象 — 田字对角，不可过河，塞象眼
  - 馬/傌 — 日字形走法，蹩马腿检测
  - 車/俥 — 直线任意距离
  - 炮/砲 — 直线移动，翻山吃子
  - 兵/卒 — 未过河只进，过河可左右前
- 将军检测 + 将死 / 困毙判定
- 无限悔棋（支持 `Ctrl+Z` 快捷键）

**🤖 AI 引擎**

| 难度 | 搜索深度 | 算法 |
|------|---------|------|
| 简单 | 2 层 | Minimax + Alpha-Beta 剪枝 |
| 普通 | 3 层 | + MVV-LVA 走法排序 |
| 困难 | ≤5 层 | + 迭代加深 + 时间保护（<1s） |

评估因子：棋子材料价值 + 位置偏好（车近底线、马近中心、炮过河）

**🎨 界面体验**

- Canvas 绘制传统棋盘（楚河漢界、九宫斜线、木质纹理）
- 红黑双方使用不同汉字（帥/將、仕/士、相/象、傌/馬、俥/車、炮/砲、兵/卒）
- 选中合法走法高亮（绿点 = 空位，红圈 = 吃子）
- 将军时被将的将/帅红色脉冲高亮
- 标准中国象棋记谱法（红方中文数字 / 黑方阿拉伯数字）
- 胜负弹窗 + 再来一局
- `Ctrl+N` 新游戏

**📜 棋谱记法示例**

```
1. 傌八進七  砲8平5
2. 俥九平八  馬2進3
3. 兵七進一  車1平2
```

### 技术架构

```
index.html（单文件，~845 行）
  ├── <style>    棋盘 + UI 样式（CSS）
  └── <script>
        ├── 规则引擎（走法生成 + 将军/飞将/合法性检测）
        ├── AI 模块（Minimax + Alpha-Beta + 迭代加深）
        └── UI 控制器（Canvas 渲染 + 事件交互 + 棋谱/弹窗）
```

- **零依赖**：无框架、无库、无网络请求
- **兼容性**：Chrome / Firefox / Edge 双击即用
- **文件大小**：~27 KB（< 200 KB 目标）

### 已知限制

| 限制 | 说明 |
|------|------|
| 长将 / 长捉 | 未实现自动判负（实现复杂度高） |
| 音效 | `file://` 协议下部分浏览器限制自动播放 |
| 棋谱同列多子 | 不区分前后字（如前馬/後馬） |

### 开发里程碑

```
Phase 1 — 核心可玩 ✅
  棋盘渲染 + 规则引擎 + 人人对战

Phase 2 — AI 对战 ✅
  Minimax + Alpha-Beta + 3 档难度

Phase 3 — 体验打磨 ✅
  将军高亮 + 棋谱列表 + 胜负弹窗
```

---

## English

### Overview

Chinese Chess (Xiangqi) is a fully offline, single-file HTML board game. No installation, no server, no internet — just download `index.html` and double-click to open in your browser.

Features a complete rule engine, 3-level AI opponent, game notation, and supports both PvP and PvAI modes.

### Quick Start

```bash
git clone https://github.com/ryukeilee/xiangqi.git
cd xiangqi
open index.html     # macOS
# Or double-click index.html (Windows / Linux)
```

Or download [index.html](index.html) directly and open it.

### Features

**🎮 Game Modes**

| Mode | Description |
|------|-------------|
| PvP | Two players take turns on the same device |
| PvAI | Play against the built-in AI with 3 difficulty levels |

**♟️ Rule Engine**

- Full legal move validation for all 7 piece types:
  - King (帥/將) — one step within the palace; flying general rule enforced
  - Advisor (仕/士) — one step diagonally within the palace
  - Elephant (相/象) — two steps diagonally; cannot cross river; eye-blocking
  - Knight (傌/馬) — L-shaped move; leg-blocking (hobbling) detection
  - Rook (俥/車) — any distance along straight lines
  - Cannon (炮/砲) — moves like rook; captures by jumping over exactly one piece
  - Pawn (兵/卒) — forward only before crossing river; forward/sideways after
- Check detection + checkmate / stalemate (both count as loss)
- Unlimited undo (`Ctrl+Z`)

**🤖 AI Engine**

| Level | Depth | Algorithm |
|-------|-------|-----------|
| Easy | 2 ply | Minimax + Alpha-Beta pruning |
| Normal | 3 ply | + MVV-LVA move ordering |
| Hard | ≤5 ply | + Iterative deepening + time limit (<1s) |

Evaluation: material + positional bonuses (rooks near opponent's back rank, knights centralized, cannons across the river)

**🎨 UI / UX**

- Canvas-rendered traditional board (river text, palace diagonals, wood texture)
- Distinct characters for red/black pieces
- Legal move highlights (green dots = empty, red rings = capture)
- Pulsing red highlight on the king when in check
- Standard Chinese Chess notation (Chinese numerals for Red, Arabic for Black)
- Victory modal with restart button
- `Ctrl+N` for new game

**📜 Sample Notation**

```
1. 傌八進七  砲8平5
2. 俥九平八  馬2進3
3. 兵七進一  車1平2
```

### Architecture

```
index.html (single file, ~845 lines)
  ├── <style>    Board + UI styles (CSS)
  └── <script>
        ├── Rule engine (move generation + check/checkmate detection)
        ├── AI module (Minimax + Alpha-Beta + iterative deepening)
        └── UI controller (Canvas rendering + events + notation/modal)
```

- **Zero dependencies**: No frameworks, libraries, or network requests
- **Compatibility**: Chrome / Firefox / Edge
- **File size**: ~27 KB

### Known Limitations

| Limitation | Notes |
|------------|-------|
| Perpetual check/chase | Automatic forfeit not implemented |
| Sound effects | Auto-play restricted under `file://` protocol |
| Notation disambiguation | Multiple same-type pieces on same column not distinguished |

### Milestones

```
Phase 1 — Core Playable ✅
  Board rendering + rule engine + PvP

Phase 2 — AI Opponent ✅
  Minimax + Alpha-Beta + 3 difficulty levels

Phase 3 — Polish ✅
  Check highlight + move notation + victory modal
```

---

[MIT License](LICENSE)
