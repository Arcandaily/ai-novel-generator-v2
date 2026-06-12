# Long-term Memory & Experience Accumulation v3.15

## 核心理念
引擎应具备**持续学习和成长**的能力。通过记录故事内的记忆和跨故事的经验，逐步提升生成质量、减少重复错误，并形成自己的“创作风格偏好”。

## 1. 记忆类型

### 1.1 故事内长期记忆（Story-Internal Memory）
记录当前故事中发生的重要事件、人物关系变化、关键决策及其后果。

### 1.2 跨故事经验库（Cross-Story Experience）
从已完成的故事或章节中提取的**通用经验和教训**，用于指导新故事的生成。

## 2. 记忆档案结构

### 2.1 故事内记忆档案
```yaml
story_id: string
key_events: list
character_relationship_evolution: object
major_decisions: list
theme_progress_log: list
emotional_highlights: list
```

### 2.2 跨故事经验库
```yaml
successful_patterns: list
common_pitfalls: list
theme_handling_experience: object
character_archetype_lessons: object
pacing_experience: object
anti_trope_experience: list
reader_feedback_summary: object
```

## 3. 记忆更新机制

### 3.1 故事内记忆更新
- 重要事件发生后立即更新
- 重大决策后更新
- 每章/每重要节点结束后进行小结

### 3.2 跨故事经验提取
Archivist 负责从已完成内容中提取经验，记录成功模式和常见问题。

### 3.3 经验应用
在生成新故事或新节点时，Planner 和 Self-Critique 应参考相关经验。

## 4. 与其他模块的结合

- **Archivist**：主要负责记忆的记录、更新和经验提取
- **Self-Critique**：在审查时参考经验库
- **Planner**：在生成分支时参考成功模式

## 5. 实施建议

1. 每完成一个重要节点或章节，Archivist 应进行小结并更新记忆。
2. 每完成一个完整故事，Archivist 应进行系统性经验提取。
3. 新故事初始化时，加载相关经验库作为约束。