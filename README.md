# plan-demine（排雷）

简体中文（本文件） | [English](README.en.md)

开工前把计划里的雷排掉：**制定计划 + 排雷一轮跑完**，不用"先出计划、等下一轮再审"。

**分工铁律：方向你定，零件 Agent 装，事实证据验。** 排雷验证的是"已拍板计划的事实"，不是 Agent 自选的方向——方向歪了，排雷只会把歪计划验证得更扎实。

## 用法

| 场景 | 命令 |
|---|---|
| 没有计划，要完整流程（定级 → 制定 → 拍板 → 排雷） | `/plan-demine` 或直接说"做个计划并排雷" |
| 已有计划文件，直接排雷 | `/plan-demine <计划文件路径>` |
| 对话里有你认可的计划（你写的、你贴的、刚拍板的） | `/plan-demine`（自动跳过制定阶段） |
| 对话里只有 Agent 刚起草、你还没拍板的计划 | `/plan-demine`（先补轻量拍板，再排雷） |

## 一轮跑完的流程

```
入口探测 → 定级（探针级 / 小改级 / 工程级）
  → 制定计划（钉方向盘；没验证过的断言当场标 [未验证]）
  → ★拍板门：你确认方向与草案（硬性，不拍板不排雷）
  → 排雷（拆雷 → 最便宜验证 → 证据表 → 分诊；只验事实，方向存疑退回你）
  → 你批准试跑清单 → 跑试跑（隔离目录，用完即删）
  → 逐条确认改动 → 回写计划 → 放行结论
```

全程被打断三次：**拍板**（防走歪的那道）、批准试跑、逐条确认改动。

## 产出三样

1. **证据表**——每条断言的状态：已证实 / 已推翻 / 未解决 / 接受的风险（没有第五种）
2. **改好的计划**——改动写进对应位置，`[未验证]` 标记摘除
3. **一句放行结论**——可以开工 / 改后可开工 / 暂不能开工

## 设计来源

- [gbasin/stress-test-skill](https://github.com/gbasin/stress-test-skill)：六阶段骨架、证据分级、三桶结论、试跑批准
- [laurigates/claude-plugins · verify-before-plan](https://github.com/laurigates/claude-plugins)：前提概念、四段返回契约、门槛过滤、最便宜验证器
- [obra/superpowers · writing-plans](https://github.com/obra/superpowers)：计划纪律（零上下文、文件结构先行、禁占位符、每步可核对）
- [obra/superpowers · brainstorming](https://github.com/obra/superpowers)：三级定级、审批门（HARD-GATE）不随任务缩水、复杂度只升不降、拍板门同源
- [github/spec-kit](https://github.com/github/spec-kit)、[eyaltoledano/claude-task-master](https://github.com/eyaltoledano/claude-task-master)：流程链与任务拆分思想

## 相关仓库

- [skill-flywheel](https://github.com/b-c-maker/skill-flywheel)：姊妹技能——任务收尾后自动把可复用流程沉淀成 skill（含反思/纠错闭环）。一本管开工，一本管收尾。

## License

[MIT](LICENSE) © 2026 b-c-maker

## 安装信息

- 位置：用户级 `~/.dsh/skills/plan-demine/`（所有工作区可见）
- 结构：顶层 `SKILL.md` + `README.md`，UTF-8 无 BOM
- 运行时产物：计划文档存 `<projectRoot>/计划/`，试跑目录 `<projectRoot>/.plan-demine-poc/`（用完删除）
