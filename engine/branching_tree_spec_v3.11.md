# 分叉树（Branching Tree）详细规范 v3.11

## 1. 设计目标
分叉树是引擎实现**可控剧情发展**和**多路径探索**的核心工具。它必须支持：
- 清晰的节点状态管理
- 逻辑依据记录
- 后果预测
- 灵活回滚
- 用户可查询和干预

## 2. 节点（Node）结构

每个节点必须包含以下字段：

```yaml
node_id: string
parent_node_id: string
status: string                  # 未经历 / 当前 / 已完成 / 已回滚
created_time: datetime
last_updated: datetime

description: string
description: string             # 节点简要描述
logic_basis: string             # 推演依据
expected_consequences: list     # 预期后果
risks: list                     # 潜在风险
alternatives: list              # 其他可行方向

related_characters: list
related_events: list

theme_impact: string
emotional_impact: string

child_nodes: list
is_major_decision: boolean
backup_snapshot_id: string
```

## 3. 树结构与生成规则

### 3.1 根节点（Root）
- 故事初始化时创建

### 3.2 节点生成时机
- 用户做出选择后
- Logical Deduction Engine 完成一轮推演后
- 重要客观事件发生后

### 3.3 节点扩展规则
- 每个节点至少应有 2-4 个合理子方向
- 子方向必须通过 6W1H + 多维度控制验证

## 4. 节点状态管理

| 状态       | 含义                     | 可操作性          |
|------------|--------------------------|-------------------|
| 未经历     | 尚未选择的可能路径       | 可选择进入        |
| 当前       | 当前正在进行的节点       | 活跃状态          |
| 已完成     | 已走完的节点             | 可查看历史        |
| 已回滚     | 已被回滚的节点           | 仅作历史记录      |

## 5. 回滚机制（Rollback）

### 5.1 支持回滚的条件
- 用户主动要求回滚到某个已经历节点
- 检测到严重逻辑矛盾或融梗风险时，系统建议回滚

### 5.2 回滚操作
- 恢复到目标节点的状态快照
- 将原路径标记为“已回滚”
- 从目标节点重新生成新的子分支

### 5.3 回滚限制
- 重大决策节点回滚需用户确认
- 回滚次数过多应记录并提示用户

## 6. 与其他模块的交互

- **State Manager**：节点变更时同步更新 novel_state.md
- **Logical Deduction Engine**：负责生成节点的逻辑依据和后果预测
- **Self-Critique**：对新生成的节点进行一致性审查
- **Controller**：负责节点状态流转和用户交互

## 7. 查询与可视化

系统应支持查询当前路径、某节点的所有子分支及状态、某人物在不同分支中的状态差异。

## 8. 实施建议

1. 重要决策必须创建状态快照。
2. 每轮推演后，Planner 应生成 2-4 个经过验证的子节点。
3. 用户可随时要求“显示当前分叉树”或“回滚到指定节点”。

---

此文档定义了分叉树的完整规范，与 `core_engine_spec_v3.1.md` 和 `novel_state_structure_v3.10.md` 配合使用。