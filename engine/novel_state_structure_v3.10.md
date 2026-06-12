# novel_state.md 详细结构规范 v3.10

## 1. 设计原则
- 状态必须**可读、可写、可回滚、可追溯**
- 所有重要字段都应有更新时间戳和变更原因记录
- 状态应支持快照（Snapshot）功能

## 2. 核心状态结构（必须包含）

### 2.1 基础信息
```yaml
project_id: string
current_version: string
last_updated: datetime
current_arc: string
current_chapter: string
word_count_target: number
current_word_count: number
```

### 2.2 时间线状态（Timeline State）
```yaml
current_time: string
time_progression_mode: string
active_time_windows: list
parallel_events: list
```

### 2.3 世界线状态（Worldline State）
```yaml
current_world_state: string
genre_core: string
world_rules: list
active_objective_events: list
butterfly_effects: list
```

### 2.4 人物状态（Characters State）
```yaml
main_characters: list
  - character_id: string
    current_status: string
    core_desire: string
    core_fear: string
    emotional_state: string
    relationship_map: object
    last_major_action: string
    last_action_time: datetime
```

### 2.5 因果链与事件记录（Causal Chain）
```yaml
major_events: list
  - event_id: string
    time: string
    who: list
    what: string
    why: string
    how: string
    consequences: list
    related_branches: list
```

### 2.6 当前分支状态（Current Branch）
```yaml
current_branch_id: string
branch_history: list
available_branches: list
last_major_decision: string
```

### 2.7 主题与情感状态（Theme & Emotion）
```yaml
core_theme: string
theme_progress: number
character_emotional_arcs: object
reader_emotional_curve: object
```

### 2.8 脑洞与特殊能力记录
```yaml
used_abilities: list
  - ability_name: string
    used_time: datetime
    cost_paid: string
    consequences: list
```

### 2.9 记忆与经验记录
```yaml
story_memory_archive: object
cross_story_experience: object
```

## 3. 状态更新规则

- 任何重要事件发生后，必须更新对应字段
- 所有更新必须记录 **变更原因** 和 **变更时间**
- 重要决策前应创建状态快照
- 支持按时间线回滚到任意快照

## 4. 状态快照规范

每次重大决策或章节生成前，系统应自动创建状态快照，包含：
- 当前完整状态副本
- 当前分支树状态
- 推演依据摘要

---

此文档定义了 `novel_state.md` 的标准结构，所有模块在读写状态时必须遵守此规范。