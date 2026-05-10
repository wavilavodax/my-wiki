# Hermes 多智能体团队构建指南

> 来源：网络文章
> 日期：2026-04-24

## 核心观点

**从单个通才到真正的多智能体团队的飞跃始于隔离，而不是更好的提示。**

- ❌ 错误思维：需要一个能做所有事情的天才 AI
- ✅ 正确思维：需要一个角色分明、交接清晰、信息污染较少的小团队

## Profiles 的隔离单位

- 配置
- 会话
- 记忆
- 技能
- 性格
- 定时任务状态
- 网关状态

## 推荐团队结构

| 角色 | Profile 名 | 职责 | SOUL.md 风格 |
|------|-----------|------|-------------|
| 协调者 | Hermes | 规划、分解、排序、综合 | 条理清晰、果断有力 |
| 研究专家 | Alan | 收集证据、核实来源、处理不确定性 | 证据至上、怀疑精神 |
| 叙事架构师 | Mira | 写作、结构、受众意识 | 清晰流畅、考虑读者 |
| 调试工程师 | Turing | 实现、调试、测试、可复现性 | 严谨准确、测试导向 |

## 操作步骤

### Step 1：确保主配置正常运行
- 模型/Provider 已配置
- API 密钥已生效

### Step 2：创建专家 Profile（使用 --clone）
```bash
hermes profile create alan --clone
hermes profile create mira --clone
hermes profile create turing --clone
```
`--clone` 会复制 config.yaml、.env、SOUL.md，但每个 Profile 仍拥有独立的内存和会话。

### Step 3：验证 Profile 存在
```bash
hermes profile list
# 或查看磁盘：
# ~/.hermes/profiles/alan/
# ~/.hermes/profiles/mira/
# ~/.hermes/profiles/turing/
```

### Step 4：编写 SOUL.md 赋予真实身份

每个 Profile 需要独立的 SOUL.md，定义：
- 语气
- 默认行为
- 优势
- 优先事项
- 应该避免什么

示例分离：
- `Hermes`：规划、委派、综合、最终质量保证
- `Alan`：证据、核实、研究深度、不确定性处理
- `Mira`：清晰表达、结构严谨、关注受众
- `Turing`：实现、调试、测试、可复现性

### Step 5：分离共享上下文

- **SOUL.md**：持久身份
- **AGENTS.md**：共享项目上下文（仓库结构、编码规范、工作流规则）

### Step 6：创建团队参考文件
```
~/.hermes/team-agents.md
```
记录：每个代理角色、交接规则、何时使用哪个 Profile。

### Step 7：运行各 Profile

```bash
hermes -p alan   # 研究专家
hermes -p mira   # 叙事架构师
hermes -p turing # 调试工程师
# 主窗口继续跑 Hermes（协调者）
```

## 关键区别

| | Profiles 多智能体 | delegate_task 子智能体 |
|---|---|---|
| 隔离单位 | 独立进程、独立内存 | 同一个上下文窗口内的临时任务 |
| 适用场景 | 长期专业化角色 | 短期并行推理/研究 |
| 状态持久性 | 各角色记忆独立积累 | 任务结束即消失 |
| 运行方式 | 多终端窗口同时跑 | 单进程内并行/串行 |

**Profiles = 养人（长期积累）**
**Delegation = 用人（用完即弃）**

## 结合消息网关

将 Profiles 与 Hermes Gateway 配合使用，可以远程监督多个 Profile，通过 Telegram 等平台分配工作，保持角色边界完整。

## 结论

最聪明的多智能体团队并非规模最大的团队，而是**角色界限最清晰**的团队。
