# USE_FOR_DP · silver-novel-skills 速查

> 本文件是 DP 知识库专用笔记，记录这套第三方小说 skills 的「能用 / 避开 / 怎么接 dp-v2 指纹体系」。
> 源仓库：`github.com/jialanhu0915/silver-novel-skills`（MIT，已克隆至 `novel/skills/silver-novel-skills/`）。
> 评估日期：2026-08-18（基于 README + character_judge / male_roles_judge / dialogue_craft / female_chapter_flow 深读）。

## 0. 定位结论

- 它是 **agent 编排型** 网文系统（Claude Code 系，带 `.claude`/`CLAUDE.md`），双系统（男频/女频）+ 框架 Agent + 多维度评测。
- **能写正文**（有 `chapter_flow` / `female_chapter_flow`），但产出的行文 AI 味重，**不能替代 dp-v2 指纹写作**。
- 真正有价值的是它的**质检层**和**框架层**，这两块你体系缺。

## 1. ✅ 直接用（接在指纹写作之后当质检/脚手架）

### 评测 Agent（最值得）
- 通用 `shared/agents/review/`：
  - `character_judge.md` — 人物塑造；**反派无脑专项**是真亮点（嘲讽须有事实/推断/立场/信息差，禁「废物/垃圾/穷鬼」人身攻击）
  - `logic_checker.md` 逻辑一致性 · `conflict_checker.md` 冲突质量 · `pace_critic.md` 节奏 · `foreshadow_hunter.md` 伏笔 · `info_auditor.md` 信息交代 · `goldfinger_checker.md` 金手指 · `climax_checker.md` 爽点 · `pov_checker.md` 视角 · `supporting_checker.md` 配角 · `plot_structure_agent.md` 结构 · `description_quality_agent.md` 描写
- 女频专项 `female/agents/review/`：
  - **`male_roles_judge.md`（Critical 级，最推荐）** — 防男主沦为女主工具人；无独立目标/完美无缺/无成长弧光/仅为奖品 直接标 Critical
  - `romance_line_judge.md` 感情线 · `bl_relationship_judge.md` · `gl_relationship_judge.md`
- 男频专项 `male/agents/review/`：`cosmic_horror_evaluator.md` · `dnd_evaluator.md`

### 框架 Agent（搭骨架用）
- `shared/agents/framework/`：`worldbuilder.md`（世界观）· `charactercraft.md`（角色弧光）· `plotarchitect.md`（情节结构）

### 结构参考（可取骨架，不取行文）
- `female/prompts/female_chapter_flow.md` 的**章节模板 + 关系阶段表 + 续写衔接检查**（查伏笔/感情线状态）
- `female/templates/`、`male/templates/` 的题材模板（金手指/打脸/感情线）——商业网文向，按需参考

## 2. ⚠️ 谨慎 / ❌ 避开（示范文风撞 dp-v2 铁律）

- `shared/templates/writing_craft/`（emotional / dialogue / scene / depth_balance / narrative_pov / world_craft）：
  - 概念可留（潜台词/留白/语言指纹/小毛病），**示范文一律别学**
  - 撞律点：`dialogue_craft` 的「嘴角勾起冷冽嘲讽」（你 banned 模板词）、「窗外没有月亮读者心凉」（D4 禁温情收束）、「三句一组均匀节奏」（D3 禁均匀）
- `female/prompts/female_chapter_flow.md` 的**「写作技巧」节** ❌：
  - 「心里像有小泡泡往上冒」= 情绪命名比喻（你 H5 禁）
  - 「每场景≥2 处微表情暗示」= 成套情绪模组（nvdi-sleuth 禁）
  - 量化指标（对话≤40%/动作≥3 处）= 装配线均匀文风
  - 情绪命名型标题（「她的心跳」）= 模板网文味

## 3. 怎么接 dp-v2 指纹体系（推荐用法）

```
① 按 dp-v2 指纹 + 多指纹组合 写正文（你的活）
② 成稿后，指定路径调用评测 Agent 做体检，例如：
   - novel/skills/silver-novel-skills/female/agents/review/male_roles_judge.md  （男主独立性）
   - novel/skills/silver-novel-skills/shared/agents/review/character_judge.md    （反派智商）
   - logic_checker / foreshadow_hunter / pace_critic 等（逻辑/伏笔/节奏）
③ 只改评测指出的结构与人设问题，行文仍由你的指纹规则掌控，不套它的 writing_craft
```

## 4. 基建缺口

- 源系统假设跑着 `shared/database/schema.sql` 的角色数据库（`characters` / `chapters` / `romance_lines` 等表）。
- **你目前没有这套基建** → `chapter_flow` 里的「先查表再写」步骤无法直接跑，只能当静态模板参考。如需真跑，要先建库并灌入角色/大纲数据。

## 5. 一句话总结

> 取它的「质检 + 框架」当工具，正文行文永远走你自己的 dp-v2 指纹；它的 writing_craft 和 chapter_flow 行文指导是 AI 味源头，别信。
