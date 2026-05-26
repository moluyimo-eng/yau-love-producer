# 丘成桐版恋与制作人 — 项目 Prompt

## 项目概要

一个纯前端 HTML 文字冒险游戏，模仿《恋与制作人》的对话+选项分支玩法，融入数学做题元素和 30+ 条丘成桐真实语录。

- **仓库**：`moluyimo-eng/yau-love-producer`（GitHub）
- **线上地址**：`https://moluyimo-eng.github.io/yau-love-producer/`
- **本地文件**：`/Users/zhihu/yau-love-producer-repo/index.html`（单文件，~1470 行）
- **技术栈**：纯 HTML/CSS/JS，无框架，GitHub Pages 部署
- **版本号**：v2.1（状态栏右侧可见）

## 核心玩法

### 结局系统：2×3 矩阵（学术 × 恋爱）

数学（学术）和好感（恋爱）是两条独立轴线：

```
              好感 65-100    好感 35-64    好感 0-34
3 题全对      卡拉比-丘之约    学术之路      黄粱一梦
0-2 题对      火速分手        恋爱未满      数学劝退
```

- **卡拉比-丘之约**：双满分才触发，结婚结局 + 全屏烟花
- **学术之路**：数学全对但好感不够高，关门弟子路线
- **黄粱一梦**：数学封神但好感冰冷，梦醒后遇蔡徐坤
- **火速分手**：好感爆表但数学崩了，约会 17 次后分手
- **恋爱未满**：中等好感但数学没全对，"保持联系"
- **数学劝退**：全线溃败，转行前端/Vibe Coding

### 好感扣减规则

- 答对数学题：+5 好感
- 答错数学题：-5 好感
- 对话选错（费马大定理）：-15
- 讲座开玩笑（霍格沃茨）：-15
- 讲座装死（假装记笔记）：-5
- 初始好感：0

### 皮卡丘 Mascot

- 状态栏有蹦跳皮卡丘 SVG
- 选错/答错时触发震屏动画 `shockPikachu()`

### 表情切换

- 正常场景：丘成桐自信微笑（YAU_SVG）
- 答错/_no/_joke/_disappointed 场景：切换为流泪悲伤版（YAU_SVG_SAD）

## 关键代码位置

| 功能 | 关键标识 |
|------|---------|
| Q 语录对象 | `const Q = {` (~30 条真实语录) |
| 丘成桐肖像 SVG | `const YAU_SVG =` / `YAU_SVG_SAD` |
| 皮卡丘 SVG | `const PIKACHU_SVG =` |
| 数学题库 | `const mathProblems = [` |
| 所有场景 | `const scenes = {` |
| 结局判定函数 | `function determineEnding()` |
| 结局数据映射 | `function getEndingData()` |
| 分享卡片生成 | `function generateShareCard()` |
| 烟花特效 | `launchFireworks()` / `#fireworks-canvas` |
| 表情切换逻辑 | `setPortrait(show, mood)` |
| 皮卡丘震屏 | `shockPikachu()` |

## 历史反馈 & 设计决策

1. **语录**：全部来自维基语录和知乎真源，融入叙事而非加标注。著名 iPhone 语录："我们的教育的确有问题。——发送自我的 iPhone"
2. **结局体系**：从 4 结局单维 → 6 结局 2×3 矩阵。因用户反馈"怎么都是学术之路"，拆分学术/恋爱为独立轴线。
3. **初始好感**：从 30 → 0。30 分预置让学术之路门槛太低。
4. **数学得分**：答对从 +10 → +5，降低数学对结局的主导权重。
5. **阈值演变**：≥2→≥1→===3（全对才算学术线）。
6. **视觉**：皮卡丘替代闪电 logo，答错表情切换，烟花全屏 fixed。
7. **知乎链接**：最终为 `https://www.zhihu.com`。

## 常见需求

- **改结局阈值**：编辑 `determineEnding()` 中的 `mathCorrect === 3` 和好感分界
- **改结局文案**：编辑 `ending_calabi_yau/_2` / `ending_scholar/_2` / `ending_quit/_2` / `ending_dream/_2` / `ending_breakup/_2` / `ending_almost/_2`
- **改结局摘要/名字**：编辑 `getEndingData()` 中的 map
- **改语录**：编辑 `const Q = {` 对象
- **加新对话/分支**：在 `const scenes = {` 中添加节点
- **改皮卡丘动画**：CSS `.pikachu-mascot` / `@keyframes pikabounce` / `shockPikachu()`
- **改分享卡片**：编辑 `generateShareCard()` 和 `badgeColors`
- **部署**：`git push origin main`，GitHub Pages 自动部署。页面右下角有版本号确认部署生效。
